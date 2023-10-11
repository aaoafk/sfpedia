---
title:      "ActiveSupport::Configurable"
date:       2023-09-17T11:21:29-04:00
tags:       ["rails", "ruby"]
identifier: "20230917T112129"
---

The `Configurable` module provides a `config` method that stores and
retrieves configuration options as an `OrderedOptions`.

```ruby
include ActiveSupport::Configurable
...
yield config
```

It's used in the Rails ecosystem but it does provide a standard
interface for dynamic configuration objects.

[Link to Rails API for
`ActiveSupport::Configurable`](https://api.rubyonrails.org/classes/ActiveSupport/Configurable.html
) 

`OpenStruct` could be used but I think piggy backing off of
`ActiveSupport::Configurable` would be better because it's purpose is
a little more fleshed out.

