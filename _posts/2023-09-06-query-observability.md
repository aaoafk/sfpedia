---
title:      "query observability"
date:       2023-09-06T21:48:32-04:00
tags:       ["database", "psql"]
identifier: "20230906T214832"
---

Queries are running all the time. How do we see what is currently running? PSQL gives us a system catalog view to do this-a view is basically a statement that is already configured to fetch some data-try:

```sql
SHOW pg_stat_activity;
```

PSQL keeps metadata inside the `pg_catalog` 