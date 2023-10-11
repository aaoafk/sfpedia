---
title:      "method search in ruby"
date:       2023-09-11T13:57:57-04:00
tags:       ["metaprogramming", "oop", "ruby"]
identifier: "20230911T135757"
---

Every object in Ruby is an instance of some class descended from
`BasicObject`. A search for a method can go up to `BasicObject`, no
matter how many classes or modules it includes.

`BasicObject` isn't where most objects get their functionality. You
should think about `Object` and the `Kernel` module that `Object`
mixes in. It's in `Kernel` as the name suggests that most base
instance methods are defined.

```ruby
class BasicObject
  # a scant eight method definitions go here
end

module Kernel
  # about 50 method definitions go here!
end

class Object < BasicObject
  # one or two private methods go here,
  # but the main point is to mix in the Kernel module
  include Kernel
end
```

Object is a subclass of BasicObject. Every class that doesn’t have an
explicit  super-class is a subclass of Object.

Method search begins in the class definition and then into any modules that the
class `includes`. Included modules are searched in reverse order of
inclusion, i.e. the most recently included is searched first. Consider
what happens if we `include` the same module multiple times?

`prepend`ing a module ensures that the methods in the module are
searched before the `class`.

`extend` makes a modules methods available on an *object*.

When `extend` is used on a *class* object it adds *class methods*.

When `extend` is used on an *instance* of an object it will add
*instance methods*

`extend`  *does not* add the module to the `class` ancestors list.
(`ClassName.ancestors`).

To resolve a message into a method, an object looks for the method in
this order: 

1. Modules prepended to its class, in reverse order of prepending
2. Its class definition.
3. Modules included in its class, in reverse order of inclusion
4. Modules prepended to its superclass
5. Its class’s superclass
6. Modules included in its superclass

If a message is not found ruby will send *method_missing* to the
receiver and the message lookup starts again but this time with
*method_missing*.
