---
title:      "factory bot association"
date:       2023-10-10T15:30:48-04:00
tags:       ["factorybot", "rails", "tdd"]
identifier: "20231010T153048"
---

Within a factory block, use the `association` method to always make an
additional object alongside this one.

`association` takes a mandatory name and optional options. The options
are zero or more `trait` names (Symbols), followed by a hash of
attribute overrides.
