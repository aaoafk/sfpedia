---
title:      "the routes object"
date:       2023-10-08T18:03:27-04:00
tags:       ["rails", "routing"]
identifier: "20231008T180327"
---

`Application.routes` is a rack application that uses the `routes.rb`
to resolve `uris` to a resolver a `Controller#action` or another
`Rack` application.

The `routes` object is an instance of
`ActionDispatch::Routing::RouteSet` class.
