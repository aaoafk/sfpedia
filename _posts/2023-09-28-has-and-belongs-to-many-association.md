---
title:      "has_and_belongs_to_many association"
date:       2023-09-28T14:52:11-04:00
tags:       ["associations", "rails"]
identifier: "20230928T145211"
---

Creates a direct *many-to-many* connection with another model, with no
intervening model.

Each instance of the declaring model refers to zero or more instances
of another model.

For e.g. if your application includes *assemblies* and *parts*, with
each assembly having many parts and each assembly having many parts
and each part appearing in many assemblies, you could declare the
models this way:

```ruby
class Assembly < ApplicationRecord
  has_and_belongs_to_many :parts
end

class Part < ApplicationRecord
  has_and_belongs_to_many :assemblies
end

# => Table name is generated using some lexigraphical ordering with
the pluralized class names.
```

**Keep in mind when creating this table that it does not represent a
model! Since it does not represent a model it does not need an `id`
column. We can enforce this with `:id => false` or by using the method
`create_join_table :model_name, :model_name`.**

The other way to delcare a *many-to-many* relationship is to use
`has_many :through`, this makes the association indirectly through a
join model.

