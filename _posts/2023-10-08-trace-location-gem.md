---
title:      "trace location gem"
date:       2023-10-08T17:48:15-04:00
tags:       ["performance", "ruby", "tools"]
identifier: "20231008T174815"
---

`trace_location` lets us track everything we would want to know about
how a program in ruby is executing.

It uses ruby's **TracePoint API** which is a runtime introspection tool.
