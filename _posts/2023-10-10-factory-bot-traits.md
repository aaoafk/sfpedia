---
title:      "factory bot traits"
date:       2023-10-10T15:29:04-04:00
tags:       ["factorybot", "rails", "tdd"]
identifier: "20231010T152904"
---

Within a `factory` definition block, use the `trait` method to define
a permutation of a factory. This usually works well for different
types of a parent factory.

```ruby
factory :user do
  ...
  trait :admin do
    # => An admin is a user with a property set
  end
end
```
