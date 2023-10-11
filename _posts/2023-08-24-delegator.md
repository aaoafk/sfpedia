---
title:      "delegator"
date:       2023-08-24T18:23:20-04:00
tags:       ["ruby"]
identifier: "20230824T182320"
---

~Delegator~ provides 3 different ways to delegate messages to objects.

The easiest to use is ~SimpleDelegator~. Pass an obj to the
constructor and all methods supported by the object will be delegated.
The object can be changed later.

~Delegator~ is also an abstract class which we can inherit to dictate
a delegating scheme, whatever that means.

There's also the other side of this called[[denote:20230824T182635][ Forwardable]].
