---
title:      "controlling association scope"
date:       2023-09-28T15:21:25-04:00
tags:       ["associations", "rails"]
identifier: "20230928T152125"
---

*Associations* look for objects only within the current modules scope.

If we declare classes in different modules then they are in different
scopes. If we want the goodies we need to use the complete
`:class_name => ModuleName::Foo`. 
