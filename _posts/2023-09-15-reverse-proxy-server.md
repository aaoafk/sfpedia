---
title:      "reverse proxy server"
date:       2023-09-15T14:10:49-04:00
tags:       ["scraping", "web"]
identifier: "20230915T141049"
---

A _reverse proxy_ is a proxy server.

A **proxy server** is a computer that forwards requests to another
computer from many clients.

A _reverse proxy_ sits behind a firewall on a private network. It's
typically used for: load balancing, web acceleration and security.

Since a _reverse proxy_ sits between two computers it can do special
things with the data before it hits a server like, caching, data
compression, ssl encryption. Keep in mind that the _reverse proxy_
routes the servers response back to the client!

A _reverse proxy_ provides security by obfuscating the IP addresses of
our server since requests are routed through it.

_reverse proxies_ are increasingly implemented in software rather than
hardware.

Examples of Reverse Proxies
---------------------------

1. **NGINX** is a _software-based_ reverse proxy solution. It does a
   lot of stuff to incoming HTTP requests before they reach our
   application servers.
