---
title:      "descendants method"
date:       2023-09-17T11:31:38-04:00
tags:       ["rails", "ruby"]
identifier: "20230917T113138"
---

`.descendants` is actually implemented by `ActiveSupport`. It is the
twin of `ancestors` which Ruby provides.

`.descendants` will give you all of the classes that inherit the
current object.

`ActiveSupport` achieves this by iterating through the `ObjectSpace`
which is exposed by Ruby and is a map of the currently executing
universe, i.e. every object that has been instantiated.

The `ObjectSpace` would be something to look into.

[HoneyBadger article explaining the `.descendants` method within the
context of ActiveSupport and Ruby method lookup](https://www.honeybadger.io/blog/hidden-gems-activesupport-descendants/ ) 
