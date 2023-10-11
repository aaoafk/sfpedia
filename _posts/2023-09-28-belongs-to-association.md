---
title:      "belongs_to association"
date:       2023-09-28T10:57:23-04:00
tags:       ["associations", "rails"]
identifier: "20230928T105723"
---

The `belongs_to` association establishes a one directional
relationship between the model that declares it and another model.

Keep in mind that the symbol provided to `belongs_to` will be resolved
to a class name and it needs to be singular.

`belongs_to` sets up an `#{singular_class_name}_id` column in the
model that declares it which links to the primary key of the other
model in the database.

The `belongs_to` association makes it so that the model that declares
it knows *who* it belongs to but the model that it references would
not know anything about *who* is referring to it. To create something
like that we would need to set up a *bi-directional association*, we
could do that by invoking `has_one` in the other model *or*
`has_many`, so that the other model would be able to access all
records that belong to it for that association.

`belongs_to` does not enforce reference consistency, depending on the
use case we may need to modify the *migration* to add a database-level
foreign key constraint on the reference column, like this:

```ruby
create_table :books do |t|
  t.belongs_to :author, foreign_key: true
end
```

[has_one association](denote:20230928T110356)
