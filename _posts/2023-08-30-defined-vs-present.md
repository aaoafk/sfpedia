---
title:      "defined? vs present?"
date:       2023-08-30T17:15:53-04:00
tags:       ["metaprogramming", "ruby"]
identifier: "20230830T171553"
---

The choice between `defined?` and `present?`. Ask yourself: "What are we trying to check?"

### `defined?`

- **Purpose**: Checks if a variable or method is defined.
- **Return value**: Returns `nil` if the expression is not defined; otherwise, returns a description of that expression.
- **Use Cases**: You want to know if a variable has been initialized or a method exists without invoking it.
  
```ruby
x = 10
defined?(x)  # => "local-variable"
defined?(y)  # => nil
```

### `present?`

- **Purpose**: Checks if an object is not `nil` and not empty (if applicable).
- **Return value**: Returns `true` or `false`.
- **Use Cases**: You want to check the existence and non-emptiness of an object, often used for strings, arrays, and hashes.

```ruby
"".present?  # => false
nil.present? # => false
[1].present? # => true
```

### When to use which?

- Use `defined?` when you want to check if a variable or method exists without actually invoking it.
- Use `present?` when you want to check if an object is both existent (not `nil`) and has some value (not empty).

#### Examples

```ruby
# Using defined?
if defined?(user)
  puts "user variable is defined"
end

# Using present?
if user.present?
  puts "user variable is both not nil and not empty"
end
```

Remember, `present?` is a Rails extension. So if you're working in a plain Ruby environment, you won't have access to it unless you bring in ActiveSupport. On the other hand, `defined?` is a Ruby built-in keyword and can be used in any Ruby environment.