---
title:      "instance_methods"
date:       2023-10-06T17:50:28-04:00
tags:       ["metaprogramming", "ruby"]
identifier: "20231006T175028"
---

`instance_methods` returns an array of methods that the receiver
supports.

It takes one argument: `include_super`. `include_super` defaults value
is true which means that methods from super classes are included.

If we pass in `false` then we will just get instance_methods that the
class of the object defines (this does **not** include singleton
methods on the **eigenclass**).
