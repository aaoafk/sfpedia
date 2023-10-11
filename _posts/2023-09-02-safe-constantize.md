---
title:      "safe_constantize"
date:       2023-09-02T11:40:12-04:00
tags:       ["metaprogramming", "ruby"]
identifier: "20230902T114012"
---

```ruby
safe_constantize(camel_cased_word)

Tries to find a constant with the name specified in the argument string

The name is assumed to be the one of a top-level constant, no matter whether it starts with “::” or not. No lexical context is taken into account:

```ruby
C = 'outside'
module M
  C = 'inside'
  C                     # => 'inside'
  safe_constantize('C') # => 'outside', same as ::C
end

nil is returned when the name is not in CamelCase or the constant (or part of it) is unknown.
