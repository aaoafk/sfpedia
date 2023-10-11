---
title:      "guide to rack for rails developers"
date:       2023-10-06T09:20:27-04:00
tags:       ["rack", "rals"]
identifier: "20231006T092027"
---

`Rack` allows us to use many web servers with one standard
interface. `Rack` is a contract between a _web server_ (puma, unicorn,
etc.) and a ruby application.

`Rack` requires a `config.ru` file, (`ru` is just an acronym for
`rackup`), in the root of a directory. The `config.ru` file should be
a Ruby class or object that fulfills the following criteria:

1. It has a `call` method.
2. It accepts the `env` object representing the `HTTP` request, it's
   just a ruby hash.
3. It returns an array containing three values: **the status code**,
   **the headers**, **the response**.
   
```ruby
# => e.g. of a `rack compliant` class
class App
  def call env
    headers = { "Content-Type" => "text/html" }
    
    response = ["<h1>Greetings from Rack!</h1>"]
    
    # => The response is an array which represents the following
    # structure: [HTTPStatusCode, HTTPHeaders, HTTPResponse]
    [200, headers, response]
  end
end
```

When we say:

> Rack provides a minimal, modular and adaptable interface

We specifically are pointing to the idea that it allows us to use many
web servers with the standard interface. The standard interface being
the file `config.ru` which defines a ruby class.

We're also pointing to the idea of the `middleware` stack.

Said another way:

> every rack compliant webserver will always invoke a `call` method on
> an object (the Rack application) and serve the result of that
> method.

`Rack` is the **HTTP pre/post processing layer** for a ruby web application.

*******

The Rack Protocol
-----------------

`Rack` is a protocol, just like `HTTP`. `Rack` provides a layer
between a `Web Server` and a `Web Application` allowing them to
communicate with each other.

`Rack` is similar to `HTTP`. In the sense that the `HTTP` protocol
allows many browsers to handle `HTTP` requests in a standardized
way.

*******

The Rack Gem
------------

There is also a `Rack` gem.

> Why do we need the Rack gem if the rack-compliant web servers and
> frameworks can communicate without it?

1. Middleware Toolbox.
2. Tools to Build Rack Applications and Middleware.
3. The `rackup` command.



*******

### Middleware Toolbox ###

*Middleware* sits between the user and the application code. `Rack`
intercepts *HTTP Requests* coming in and *HTTP Responses* going out.

The `Rack` gem provides implementations of middleware:

* `Rack::Files` for serving static files.
* `Rack::Config` for modifying the environment before processing the
  request
* `Rack::ContentLength` for setting `content-length` header based on
  the body size.
* `Rack::Deflater` for compressing responses with `gzip`.

Consult the `Rack` documentation for other implementations of
middleware.

**The design of `Rack` is modular so that we can inject as many
middleware as we want into our stack.** 

We can see the middleware stack in a Rails application with:

`bin/rails middleware`

`Rails` gives us full control of the middleware stack allowing us to
add, remove or rearrange middleware.

There are also some implementations here: [Implemented Rack
Middleware](https://github.com/rack/rack-contrib) 

*******

### The `rackup` command ###

The Rack gem ships with the `rackup` command. Since `Rack 3` the
`rackup` command has been moved to a separate `rackup` gem. It's a
tool for running `Rack` applications with a web server. It uses the
`Rack::Builder` DSL to configure middleware and compose applications.

`rackup` automatically figures out the environment it is run in, it
will run our application using `WEBrick`, `Puma`, or any web server

### References ###

[Link to Akshay Khot
article](https://www.akshaykhot.com/definitiive-guide-to-rack/ ) 
