---
title:      "Load Balancing"
date:       2023-06-20T11:31:00-04:00
tags:       ["systemdesign"]
identifier: "20230620T113100"
---

Load Balancing is the distribution of many requests across resources.

It's a field of research in parallel computers. There are two
approaches: static algorithms and dynamic algorithms.

This can get complicated when you consider how we can track how a task
is done. A task requires CPU time. If tasks are all of the same size
then it's trivial to know when a task is done. However, if tasks are
of varying sizes then it becomes difficult.
