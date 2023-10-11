---
title:      "Rails initializers"
date:       2023-08-16T13:56:46-04:00
tags:       ["rails"]
identifier: "20230816T135646"
---

An initializer is just ruby code in ~config/initializers~ directory.
We use initializers to configure Rails application or external gems.

~bin/rails initializers~ lists the initializers and what order or
~bundle exec rails initializers~ to execute within the context of the
`Gemfile`.
