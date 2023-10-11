---
title:      "unbound methods"
date:       2023-04-18T11:31:55-04:00
tags:       ["closure", "metaprogramming", "methods", "ruby"]
identifier: "20230418T113155"
---

UnboundMethods are like Methods that have been detached from their
original class or module. You can turn a Method into an UnboundMethod
by calling Method#unbind. You can also get an UnboundMethod directly
by calling Module#instance_method.

You can bind an UnboundMethod with Method#bind. If you're binding to
an instance of a class it needs to respond true to Kernel#class? or
Object#kind_of?

You can bind an UnboundMethod by passing it to Module#define_method
