---
title:      "sharing role behavior with modules"
date:       2023-09-14T14:29:57-04:00
tags:       ["oop", "ruby", "softwaredevelopment"]
identifier: "20230914T142957"
---

Classical inheritance only allows a class to inherit methods from only
one `superclass`. Many OOP languages offer a way to add methods to an
object via another means, in ruby that's done with a `module`. Keep in
mind that *classes* are just objects too.

A `module` is another way to add *methods* to any object in ruby. In this sense
they can be treated like *classical inheritance* this means that we
can kind of follow the same rules as those in *classical inheritance*,
the *template method pattern* should be followed, i.e. the `module`
should provide its own default. *hook methods* can be used to avoid
forcing an *includer* to send `super`.

There is one thing that we should keep in mind though, **when
different classes need to share behavior we implement that in a
`module`**. 

Some *roles* are obvious at design time others reveal themselves as we
code. *duck types* are *roles*. It is common to discover *roles* where
the commonality is not just a *method signature* but also an
implementation of specific behavior.
