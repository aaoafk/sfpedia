---
title:      "Postgres roles"
date:       2023-08-15T14:42:12-04:00
tags:       ["psql"]
identifier: "20230815T144212"
---

PostgreSQL manages database access permissions using the concept of
roles.

A role is a DB user or a group of users.

Roles can own DB objects (e.g. tables) and can assign privileges on
those objects to other roles to control who has access to which
objects.

DB roles are global across an instance.

```sql
create role <ROLE_NAME>;
```

<ROLE_NAME> is a SQL identifier: either unadorned without special
chars or double-quoted.

We can drop a role with:

```sql
drop role <ROLE_NAME>;
```

We can get all roles with:

```sql
select rolname from pg_roles;

```

By default, `postgres`, is a role that should be available on any
database installation unless it was changed with `initdb`. Login as
that user to make other changes with: `sudo su postgres`.
