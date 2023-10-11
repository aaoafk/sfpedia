---
title:      "super keyword"
date:       2023-09-11T14:14:36-04:00
tags:       ["metaprogramming", "oop", "ruby"]
identifier: "20230911T141436"
---

Inside a method definition we can jump up to the next method definition in
the lookup path with `super`. Why would you want to do this?

 Called with no argument list (empty or otherwise), super automatically for-
wards the arguments that were passed to the method from which it’s called.

 Called with an empty argument list—super()—super sends no arguments to
the higher-up method, even if arguments were passed to the current method.

 Called with specific arguments—super(a,b,c)—super sends exactly those
arguments.
