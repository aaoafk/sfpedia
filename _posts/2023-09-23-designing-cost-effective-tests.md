---
title:      "Designing Cost-Effective Tests"
date:       2023-09-23T14:02:47-04:00
tags:       ["oop", "softwaredevelopment"]
identifier: "20230923T140247"
---

Test the most stable part of an object and that is its *public
interface*. Don't couple your tests to the internals of an object
because those are the most subject to change.

Some outgoing messages have no side effects and these are called
*query messages*. Query messages don't need to be tested.

*Command messages* are messages that do have side effects, a database
record is written, a file is written, etc.) These kinds of messages
should be tested and it is the responsibility of the sending object to
**prove** that they are properly sent.

Proving that a message gets sent is a test of behavior, not state, and
involves assertions about the number of times, and with what
arguments, the message is sent.

Here are guidelines for what to test:

1. Incoming messages should be tested for the state they return.
2. Outgoing *command messages* should be tested to ensure they get
   sent.
3. Outgoing *query messages* should not be tested.

----------

### Testing Private Methods ###

The rules of thumb for testing private methods are:

1. Never write them
2. If you do write them, never test them unless it makes sense to do
   so
3. Therefore, be biased against writing these tests but do not fear to
   do so if this would improve your lot.

----------

### Testing outgoing messages ###



