---
title:      "web scraping"
date:       2023-09-15T13:55:43-04:00
tags:       ["nobee", "ruby", "softwaredevelopment", "web"]
identifier: "20230915T135543"
---

# High Performance Web Scraper for Ruby

----------

# Overview #

A crawler should fulfill these qualities:

1. **Distributed**
2. **Scalable**
3. **Performant and efficient**
4. **Fulfill some *freshness* heuristic**
5. **Extensible**

*DNS Resolution* is a bottleneck because it can involve many frames of
network traffic in order to resolve a hostname to an ip address. This
needs to be done asynchronously. Ruby implements *async-dns* for this.

----------

## System Architecture

System is partitioned into a *crawling system* and *crawling
application*. 

The *crawling system* is based on these components:

1. A `CrawlManager`, **central component of the system**
2. A `CrawlApplicatoin`, which forwards URL requests to the manager
3. One or more `Downloaders`
4. One or more `DNSResolvers`

There is also a web interface that the `CrawlManager` interacts with.

A `Downloader` is an async http client that is capable of downloading
hundreds of web pages in parallel.

A `DNSResolver` is a optimized stub DNS resolver that forwards queries
to local DNS Servers.

Communication in our system is done in two ways: via sockets for small
messages and via file system (NFS) for larger data streams. The use of
NFS in particular makes the design very flexible and allows us to tune
system performance by redirecting and partitioning I/O between disks.
All of these components, plus the crawling application, can run on
different machines (and operating systems) and can be replicated to
increase system performance.

### The `CrawlManager` ###

The **CrawlManager** is the only object visible to every other object
in the system. It has these responsibilities:

1. Receives requests for URL(s) from the `CrawlApplicatoin`. 
2. Each Request has a priority level, and a pointer to a file
   containing records of other URL(s), the file is located on some
   disk accessible via NFS. 
3. The manager will `enqueue` the request, and will eventually load
   the
4. After loading the URLs of a request files, the manager queries the
   DNS resolvers for the IP addresses of the servers, unless a recent
   address is already cached. 
5. Then we get the *robots.txt* file. (*robots.txt* is just a policy
   for bots to follow. If we pay attention to it that is. We still
   want some of the data that is in there though, like `sitemap.xml`)
6. Robot files are written to a separate directory from the other data
   so that they can be accessed and parsed by the manager later.
7. Finally, after parsing the robots files and removing excluded URLs,
the requested URLs are sent in batches to the downloaders, making sure 
that a certain interval between requests to the same server is
observed. 
8. Manager then notifies the application of the pages that have been
   downloaded and available for processing.
9. The manager is also in charge of limiting the overall speed of the
crawl and balancing the load among downloaders and DNS resolvers, by
monitoring and adjusting DNS resolver load and downloader speed as
needed. The manager performs periodic snapshots of its data
structures, and after a crash, a limited number of pages may have to
be recrawled. It is up to the application to detect these duplicate
pages.

----------

### Downloaders and DNS Resolvers ###

`Downloader` is concurrent and opens up many connections to different
web servers it polls those connections for arriving data. Data is then
marshaled into files located in a directory that is determined by the
application and accessible via NFS.

A large number of pages are written out to the disk in one operation.
The way pages are written to these data files **does not** parallel
the request files that the application sends.

The `CrawlManager` can adjust the speed of a `Downloader` by changing
the number of concurrent connections that are used.

The `DNSResolver` uses GNU `adns`, which is an asynchronous DNS
client, as mentioned earlier, we're gonna use `gem "async-dns"`

Downloaded files are forwarded to a storage system for compression and
storage in a database. We could use `gzip` for this or `brotli`.
Possibly doing this with a `compressable` concern.

----------

### `CrawlingApplication` ###

`CrawlingApplication` is a *Breadth-First* crawl starting out at a set
of seed URL(s).

The `CrawlingApplication` parses pages for information, checks whether
the URL(s) have been encountered before, and if they have not been
encountered, sends them to the `CrawlManager` in batches.

The downloaded files are then forwarded to a storage manager for
compression and storage. The `CrawlingApplication` is implemented in
C++ using STL and the Red-Black Tree implementation in the `ka-zlib`
library. The application consists of two threads using the structure,
whichever structure we use, it needs to be thread-safe.

Sometimes pages have similar content which we can use a
*fingerprinting* technique to avoid parsing the same page, but some
pages are actually *virtually* the same to address this you can use
*shingles*.

The *URL Seen* data structure keeps track of the URLs that we have
encountered. A *URL* if stored in memory as a string will take up
around 50 bytes. Figure that we could store around 20,000,000 URL(s)
in a GB with this average size. Currently, I have 185 GB free on my
computer: that is 185 * 20,000,000 = 3,700,000,000 URLs.

----------


**We need to maximize leads...** 

IDX Feeds are important.

Web scraping is legal but not all websites allow it because it burdens
web servers. 

----------

We can see if a website allows scraping by appending `/robots.txt` to
the sites *URL*.

----------

Websites **WILL** block you for scraping. There are ways to get around
this, e.g. proxies.

There is definitely a dearth of scraping tools in ruby. Most of this
stuff is done with Python.

[Scrapy python implementation](https://github.com/scrapy/scrapy ) 

----------

We need to store the state of URL(s) that we want to hit. We could
store that in a database.

The database could have a table of URL(s) with columns based on the
last time that the URL was hit. *This would serve as a heuristic for
when to scrape that website again*.

We will also have a database of address records that belong to a URL
resource.

Schema:

country => Country (always required, 2 character ISO code)
name_line => Full name (default name entry)
first_name => First name
last_name => Last name
organisation_name => Company
administrative_area => State / Province / Region (ISO code when available)
sub_administrative_area => County / District (unused)
locality => City / Town
dependent_locality => Dependent locality (unused)
postal_code => Postal code / ZIP Code
thoroughfare => Street address
premise => Apartment, Suite, Box number, etc.
sub_premise => Sub premise (unused)

TODO: read about **xNAL** standard but here is the database definition
for the addresses.

```sql

```

We need to create an interface for the `Address` data model. Use
`Sequel::Model` for this.

```ruby
gem 'sequel'
```

----------

Websites could provide a: `sitemap.xml` to indicate the last modified
for a web page. If this file exists it *could* be used to determine
when an address record *could* be different.

In the case that it does not exist though. What could we do?

1. Take a hash of the webpage and store it in a table and use that to
   determine when a web page has changed.

When we're updating a set of address records for a URL we will need to
scrape the webpage and compare the set of freshly scraped addresses to
the ones in the database. There are a couple of ways that an update
can happen:

1. We have a new address that we have never seen before
2. We have an address that we *have* seen before but that needs to be
   updated.

Regardless we will need a way to compare an address data structure and
to do that we can use `comparable`. We need to find an accurate basis
of comparison.

```ruby
Address = Data.define(...) do
  def <=>(other)
    ...
  end
end
```

----------

#### Misc ####

Web contains servers that create *spider traps*, which are generators
of web pages that mislead crawlers into getting stuck fetching an
infinite number of pages in a particular domain. Crawlers should be
resilient to such traps. Not all of these traps are malicious and some
are just due to bad website design.

I'm just gonna go ahead and do a `Compressable` implementation because
it would be nice to have that quality for any kind of piece of data.

I also want to make sure that the interface supports persisting the
data to a database. That should be easy with just a database url. 

We could add support in Rails through a `Railtie`.

----------

### References ###

1. [Introduction to Information
Retrieval](https://nlp.stanford.edu/IR-book/html/htmledition/irbook.html) 

2. [Design and implementation of a high-performance distributed web-crawler](https://cse.engineering.nyu.edu/tr/tr-cis-2001-03.pdf) 



