---
title:      "autoloading"
date:       2023-08-26T11:53:07-04:00
tags:       ["files", "rails", "ruby"]
identifier: "20230826T115307"
---

`autoload` is used to load a file just when we need it. What does that
mean?

It means that we register a _filename_ to be loaded using
`Kernel::require` the first time that a `const` (which may be a string
or symbol is accessed).

```ruby
    autoload :Foo, "/the/path/to/foo.rb"
```

There are slightly different implementations:

1. `Module` implements it with the caveat that the file will be loaded
   whenever the `const` is accessed within the namespace of mod.

2. `ActiveSupport` also implements it.
