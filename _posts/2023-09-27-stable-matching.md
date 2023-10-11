---
title:      "stable matching"
date:       2023-09-27T10:20:23-04:00
tags:       ["algorithms"]
identifier: "20230927T102023"
---

*Issue*: Is it possible to design a system that is *self-enforcing* by
taking *self-interest* into account?

Gale-Shapley first considered this in 1962 when it came to matching up
colleges to students.

The problem has these properties:

1. Each group has a list of preferences for elements in the other
   group.
2. We need to pair people up such that:

*E* prefers every one of its accepted applicants to *A*; or, A prefers
their current situation over working for another employer.

If the above holds we call the outcome stable: *individual
self-interest* will prevent a deal from being made behind the scenes
and introducing an *instability*.

Following Gale and Shapley, we observe that this special case can be
viewed as the problem of devising a system by which each of n men and
n women can end up getting married: our problem naturally has the analogue
of two “genders”—the applicants and the companies—and in the case we are
considering, everyone is seeking to be paired with exactly one individual of
the opposite gender.

Gale & Shapley considered the same-sex Stable Matching Problem as
well, where there is only a single gender.

A matching set `S` is a set such that every man in `M` and every woman
in `W` appears in at most one pair of `S`.

A perfect matching set `S'` is a set such that every man in `M` and
every woman in `W` appears in exactly one pair, i.e. no one is left out.

----------

### Designing the algorithm ###

**There exists a stable matching for every set of preferences lists
among the men and women.**

The way that we show this will answer two questions:

1. Does there exists a *stable matching* for every set of preference
   lists?
2. Given a set of preference lists, can we efficiently construct a
   *stable matching* if there is one?
   
   
#### Gale-Shapley Algorithm ####

```
Initially all m ∈ M and w ∈ W are free
While there is a man m who is free and hasn’t proposed to
every woman
	Choose such a man m
	Let w be the highest-ranked woman in m’s preference list
	to whom m has not yet proposed
	If w is free then
		(m, w) become engaged
	Else w is currently engaged to m′
		If w prefers m′ to m then
			m remains free
		Else w prefers m to m′
			(m, w) become engaged
			m′ becomes free
		Endif
	Endif
Endwhile
Return the set S of engaged pairs
```

The question is how can we prove that this returns a *stable
matching*, or even a *perfect matching*?

----------

### Analyzing the algorithm ###
