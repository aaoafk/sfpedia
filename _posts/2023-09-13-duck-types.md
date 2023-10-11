---
title:      "duck types"
date:       2023-09-13T15:39:42-04:00
tags:       ["oop", "ruby", "softwaredevelopment"]
identifier: "20230913T153942"
---
So far we've learned that focusing on messages allows us to build
applications that are more flexible and ready for the changes that the
future might require.

`duck types` focus on finding a public interface that exists between
classes, what Metz often refers to as a *role*. Metz, and probably
others, emphasize that dependencies on `duck types` are more
sustainable than dependencies on `classes`. 

`duck types` allow us to shift our focus from the `type` of a specific
piece of data towards a focus onto a property that is shared between
many different kinds of things.

> Use of a duck type moves your code along the scale from more
> concrete to more abstract, making the code easier to extend but
> casting a veil over the underlying class of the duck.The ability to
> tolerate ambiguity about the class of an object is the hallmark of a
> confident designer.

This is also known by a more loaded term `polymorphism`, many (poly)
forms (morph) of objects respond to the same message.

Finding ducks is hard here are some clues that we might be dealing
with an undiscovered duck:

1. Case statements that switch on `class`.
2. `kind_of?` and `is_a?`
3. `responds_to?`

>The purpose of design is to lower costs; bring this measuring stick every situation. If creating a duck type would reduce unstable dependencies, do so. Use your best judgment.

`duck types` require embracing dynamic behavior. `duck types` also
bring to mind the dynamic vs static programming languages debate.

Basically, *static* typed languages require that the category of a
piece of *data* be announced, during variable declaration and in
method arguments. These languages also have compilers that perform
type-checking for you and announce errors when incompatible messages
are sent to specific kinds of receivers.

Static typed languages don't prevent type errors, e.g. we can cast a
value in a statically typed language and the compiler will take a step
aside.

