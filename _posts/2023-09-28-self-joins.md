---
title:      "self joins"
date:       2023-09-28T15:05:28-04:00
tags:       ["associations", "rails"]
identifier: "20230928T150528"
---

In designing *data models* sometimes we come across models that should
have a relation to themselves.

For example: we want to store employees in a single table and set up
*managers* and *subordinates* in that table too.

This can be modeled with self-joining associations.
