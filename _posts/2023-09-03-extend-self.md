---
title:      "extend self"
date:       2023-09-03T19:59:46-04:00
tags:       ["ruby"]
identifier: "20230903T195946"
---

We can add class methods to modules in many different ways.

One trick is to `extend self` at the beginning of a module declaration, but how does this work if instance methods haven't been defined yet?

This works because of ruby's two-pass approach. When ruby loads a file it first constructs the AST (Abstract Syntax Tree) which is a representation of the code structure.

An AST is just a data structure that corresponds to a programs structure.

Ruby notes that `extend self` will be called at some point but it is not evaluated until run-time. When we're at run-time all the instance methods would have been defined and we get all our class methods.
