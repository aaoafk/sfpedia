---
title:      "creating flexible interfaces"
date:       2023-09-09T14:10:33-04:00
tags:       ["ruby", "softwaredevelopment", "oop"]
identifier: "20230909T141033"
---

There are two kinds of interfaces:

1. The interface that a class implements and comprises the set of
   messages it supports.

2. The interface that is classless, i.e. the one that is an
   abstraction rooted in a shared message that exists between classes
   think: `sort`. Elements can `sort` themselves but a order may mean
   different things based on the set of elements! (You should think
   *Duck Typing*)

Classes have public interfaces that depend on private interfaces. (In
ruby we can access private methods whenever we want though)

We should reframe our thinking from: "I know I need this class, what
should it do?" to, "I need to send this message, *who* should respond
to it?", **we have objects because we have messages that we want to
send**

There is a distinction between a message that *orchestrates* behavior
and a message that *asks* for something to be done. This point is
usually parallel to large public interfaces; large public interfaces
usually expose the fact that an objects behavior is dictated by
something other than itself.

> Construct public interfaces with an eye toward minimizing the context they require from others. Keep the what versus how distinction in mind; create public methods that allow senders to get what they want without knowing how your class implements its behavior.

When we design our classes we should strive for `context independece`.
Accomplishing `context independence` is difficult. After all, is it
not the case that an object *must* know something about another object
when it is collaborating? Meditate on the e.g. where Metz passed in
`self`, its kinda like *dependency injection*.

In summary, applications are all about messages. Messages are
expressed in public interfaces. The state of our public interfaces may
reflect how coupled our domain objects are.

We should focus on messages because they often reveal objects that are
waiting to be implemented. When messages are *trusting* and ask for
what the sender wants instead of telling the receiver how to behave
lead to flexible public interfaces that can be reused in exciting
ways.

[Forwardable](denote:20230824T182635)
[delegator](denote:20230824T182320)
[the law of demeter](denote:20230912T175848)
