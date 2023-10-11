---
title:      "combining objects with composition"
date:       2023-09-20T08:56:43-04:00
tags:       ["oop", "ruby", "softwaredevelopment"]
identifier: "20230920T085643"
---

Composing objects requires us to think of objects that play *roles*
and the *has a* relationship that forms between objects as a result of
this.

**Objects that play a role don't need to be a kind-of that class they
just need to respond to the same set of messages! Things brings to
mind the concept of a duck type**

**Aggregation** is a special kind of composition. **Aggregation**
still fulfills the *has a* relationship between two things, but it
separates the objects life from the object which is serving as the
container.

This is because *composition* in the strict definition of the term
also defines a lifecycle relationship between two objects, i.e. the
composed object has objects that play a role for it and once the
composes object is gone then so is everything else.

A composed object like a meal has an appetizer, entree and dessert.
Once the *Meal* is gone then so are all the objects which it's
composed of. (**Composition**)

A University *has many* departments which *have many* professors. When
a University is gone then so are all of its departments but when a
department is gone this doesn't mean that all the professors are
obliterated. (**Aggregation**)

Remember that whether we're using *classical inheritance* via a *is-a*
relationship or composition via a *has a* relationship or duck types
via a *behaves like a* relationship; these are all *code arrangement
techniques* they are measuring sticks that should be applied to
contexts with our best judgement.

Briefly:

1. *Classical inheritance* provides *automatic message delegation* to
   *superclasses* but if we get our hierarchy wrong then we risk
   getting subclasses that need to implement their own behavior and
   this will propogate objects that need to be understood
   individually!

2. *Composition* leads to objects that don't have a dependency on
   their superclass but require explicit delegation of messages to the
   objects that it's composed of.
   
Roughly that seems to be the best way to summarize these ideas.
