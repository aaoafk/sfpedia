---
title:      "has_one association"
date:       2023-09-28T11:03:56-04:00
tags:       ["associations", "rails"]
identifier: "20230928T110356"
---

The `has_one` pretty much does the same thing as a `belongs_to` but in
the opposite direction, i.e. it adds the `id` reference to the *other*
model.

Depending on the use case, we might need to create a unique index
and/or a foreign key constraint at the database-level.

**This is actually an important point. We are responsible for
enforcing referential integrity at the database level! Keep this in
mind when we're developing.**

```ruby
create_table :accounts do |t|
  t.belongs_to :supplier, index: { unique: true }, foreign_key: true
end
```

This relation *could* be *bi-directional* when used in combo with
`belongs_to` on the other model.

[belongs_to association](denote:20230928T105723)
