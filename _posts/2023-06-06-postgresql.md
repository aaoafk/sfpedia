---
title:      "PostgreSQL"
date:       2023-06-06T14:50:13-04:00
tags:       ["psql"]
identifier: "20230606T145013"
---

PostgreSQL follows a client/server model. Clients and servers are just
computers. The client and servers can be on different hosts and they
talk through a TCP/IP network connection. The PostgreSQL server can
handle multiple parallel connections from clients. To do this it
`forks` a new process for each client. The original `postgres`
supervisor process is always running, waiting for clients to connect.

PostgreSQL user accounts are different from operating system accounts.
We can use the `-U` switch or set the $PGUSER environmental variable.

If you do not specify a database name when using the `psql` command it
will default to your user account name. To get help on the syntax of
various psql commands use `\h` inside the psql shell, te get out of
psql type `\q`.

`psql --list` will list all databases in a nice table.

These are meta commands:

\list or \l: list all databases
\c <db name> <user name>: connect to a certain database
\dt: list all tables in the current database using your search_path
\dt *.: list all tables in the current database regardless your search_path
\x -> Get better display for long output, "expanded output"

So what we know from SQL Server applies to psql too. I mean there are
data pages, we can see those with the `SHOW data_directory` command.
