---
title:      "Active Record"
date:       2023-08-16T17:12:46-04:00
tags:       ["rails"]
identifier: "20230816T171246"
---

ActiveRecord is an e.g. of an ORM. An ORM is just a concept for
representing objects that can talk to a database system.

In ActiveRecord a class name is pluralized to map to a database table,
e.g. a model with the name Book would map to a database table called
books, the database table is represented in _snake_case_ and the model
name is _CamelCase_, like any other class in ruby, Rails knows how to
deal with words that have irregular forms in the plural, e.g. Person
model would map to a database table called people.

ActiveRecord supports CRUD, creating, reading, updating and destroying
via a set of methods.
