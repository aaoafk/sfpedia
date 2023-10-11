---
title:      "acquiring behavior through inheritance"
date:       2023-09-14T13:02:05-04:00
tags:       ["oop", "ruby", "softwaredevelopment"]
identifier: "20230914T130205"
---

The idea of inheritance at its core is `automatic message delegation`.

It creates a relationship between objects such that a message that is
not understood is forwarded along.

In classical inheritance, this is done by Superclass <-> Subclass,
classical here is a play on the word *class* not something that is
traditional or old.

There are other inheritance techniques. JavaScript supports
*prototypical inheritance* and Ruby has *modules*.

An indicatoin that we may haven an `embedded type`, something that has
not been properly refactored into a subclass, is when we have code
that is drawing a distinction between categories of the same object.
Sometimes this reveals itself in an *antipattern*--a pattern of a bad
kind of thing--where code is checking an attribute that checks the
category to determine which message to send.

This is similar to the *antipattern* that reveals an undiscovered
`duck type`, `duck types` being more concerned with the `message`
which needs to be sent without knowledge of the type of the receiver.

> In each case, if the sender could talk, it would be saying, “I know who you are, and because of that, I know what you do.” This knowledge is a dependency that raises the cost of change. 

Always keep in mind that *subclasses* are **specializations** of a
*superclass*, this means that it has all the behavior that the
*superclass* has and *more*.

It's easier to promote code to a *superclass* than to move code to a
*subclass*. Always ask yourself, 
>"What will happen if I'm wrong?"

Meditate on the difference between pushing all the abstract code down
into the concrete class and then bringing the abstract messages back
up vs. extracting only concrete messages into the subclass and leaving
abstract messages in the abstract class.

We can use the *template method pattern* to assign default values.
*template methods* are implemented inside the *superclass*. The
*superclass* provides its own implementation, the default value, but a
*subclass* can override it to provide its own value. It's good
practice to implement every *template method* even if the *superclass*
implementation just throws an error.

Hook methods reduce coupling between the abstract superclass and a
subclass by removing the need to send `super`. This removes the
understanding of the *abstract algorithm* from the concrete class.

We could find issues with this but if we keep in mind the assumption
that the abstraction is concrete and stable then a lot of the issues
melt away.

