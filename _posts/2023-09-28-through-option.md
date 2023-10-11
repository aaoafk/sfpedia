---
title:      ":through option"
date:       2023-09-28T14:46:56-04:00
tags:       ["associations", "rails"]
identifier: "20230928T144656"
---

The `:through => :model_name` declares a third table that we can
associate this model too.

Meditate on the following:

```ruby
class Person < ApplicationRecord
  has_one :physician # => add `person_id` to physicians table
  has_one :hospital, :through => :physician # => retrieve hospital
  through `physician_id` on hospitals table
end
```
