---
title:      "sending circus"
date:       2023-09-20T22:51:05-04:00
tags:       ["metaprogramming", "ruby"]
identifier: "20230920T225105"
---

`public_send` is like `send` except it can only invoke a method that
is explicitly *public* in `self` interface.

```ruby
class Foo
  def hello
    puts "hello"
  end
end

ifoo = Foo.new
ifoo.public_send :hello # => "hello"
```

`send` just invokes the method that is passed in and passes any args
specified. If the method name is passed in as a `string` it is
converted to a `symbol`.

`BasicObject` implements `__send__`. `Kernel` implements `send`.
`__send__` is safer than `send` when the object also implements a
`send` message, e.g. `Socket`.
