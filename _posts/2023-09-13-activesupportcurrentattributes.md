---
title:      "ActiveSupport::CurrentAttributes"
date:       2023-09-13T18:07:18-04:00
tags:       ["rails"]
identifier: "20230913T180718"
---

`ActiveSupport::CurrentAttributes` is a way to make a global object
available in the entire system. It resets on a per-request basis.
I'm going to expand on the specific use case later but you can always
google it.

Apparently it shouldn't be used for things outside of *user*,
*account* and *request details* since it makes it easy to mangle your system.
