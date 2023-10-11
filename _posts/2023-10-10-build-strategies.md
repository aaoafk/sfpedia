---
title:      "build strategies"
date:       2023-10-10T15:40:36-04:00
tags:       ["factorybot", "rials", "tdd"]
identifier: "20231010T154036"
---

Once a factory is defined, it can be constructed using any of the
built-in build strategies, or a custom build strategy.

All of these strategies notify on the `factory_bot.run_factory`
instrumentation using `ActiveSupport::Notifications`, passing a
payload with `:name, :strategy, :traits, :overrides, :factory`
