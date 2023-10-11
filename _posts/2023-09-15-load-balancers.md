---
title:      "load balancers"
date:       2023-09-15T14:34:33-04:00
tags:       ["web"]
identifier: "20230915T143433"
---

A _load balancer_ is a computer that distributes requests across
computers. 

A _load balancer_ is often confused with a _reverse proxy_ but they
are different.

A _load balancer_ is usually deployed only when you need to scale up,
i.e. you're receiving so many requests that your server is literally
erroring out because of the load.

A _load balancer_ often checks if your application servers are up, via
something like a _health check_, and distributes requests based on
computers that it knows are good to go.

Keep in mind that some _load balancers_ are aware of **session
persistence**. Although HTTP is a stateless protocol, web applications
sometimes need to keep track of a users session in order to do stuff,
but if a _load balancer_ routes a request its seen before to a
different computer than computer that has the session state we'll have
issues. 

While a _reverse proxy_ is more like the "public face" of your
website. 

Its address is the one advertised for the website, and it sits at the
edge of the site’s network to accept requests from web browsers and
mobile apps for the content hosted at the website.
