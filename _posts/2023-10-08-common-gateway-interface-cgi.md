---
title:      "Common Gateway Interface (CGI)"
date:       2023-10-08T17:31:10-04:00
tags:       ["http", "web"]
identifier: "20231008T173110"
---

**Common Gateway Interface** was the first attempt to define an
interface for communication between web servers and applications. A
CGI compliant program should read request headers from `env`
variables, the request body from `STDIN`, and write the response to
`STDOUT`.

A `CGI` web server runs a new instance of the program for every
request - an unaffordable luxury for today's `Rails` applications.

`FastCGI` was created to resolve this performance issue.
