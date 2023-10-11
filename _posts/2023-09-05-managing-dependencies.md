---
title:      "managing dependencies"
date:       2023-09-05T10:52:22-04:00
tags:       ["ruby", "softwaredevelopment"]
identifier: "20230905T105222"
---

Objects have to know about each other and knowing is a dependency. An object has a dependency when:

1. It knows the name of another class.
2. The name of a message to send to someone other than `self`.
3. The arguments required for a method.
4. The order of these arguments if we're using `positional arguments`.

`Dependency Injection` is a way to deal with 1). `Dependency
Injection` is just passing in an object that will respond to the
message that we expect. `Dependency Injection` relies on our ability
to differentiate between the message that needs to be sent vs. the
type of a object or data structure. Basically, we *must* have a
dependency but *where* we implement it matters. Obviously we're gonna
put that dependency somewhere and the *where* does matter. 

If we can't use `Dependency Injection` then we should try to isolate the reference to the external class. How could we do this?

Metz holds that the next kind of dependency to manage are messages to
objects other than `self`. We do this by converting messages to other
objects INTO messages to `self`. 

Use Keyword Arguments to resolve 3 & 4.

`Dependency Direction` deals with concreteness vs. abstractness. When
we're implementing our interface we want to try to depend on
abstractions, that is on `ducks`, because `ducks` usually deal with a
quality that is shared between many different things, it's supposed to
be a better thing to lean on in the uncertain future. 

`Depend on things that change less often than you do` is the heuristic
that stands in for all the ideas in this section and a good heuristic
for life.

Injecting dependencies creates loosely coupled objects that can be
reused in novel ways. Isolating dependencies allows objects to quickly
adapt to unexpected changes. Depending on abstractions decreases the likelihood of facing these changes.
