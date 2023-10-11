---
title:      "module ClassMethods"
date:       2023-08-30T16:29:21-04:00
tags:       ["metaprogramming", "ruby"]
identifier: "20230830T162921"
---

In Ruby, modules are used to encapsulate methods, constants, and class variables that can be mixed into classes. When you include a module in a class, you are essentially adding that module's methods, constants, and class variables to that class. However, the way the methods are added can be different based on whether they are instance methods or class methods.

### `module InstanceMethods`

When you define methods within a module and then include that module in a class, the methods get added as instance methods of the class. This is the most straightforward usage of modules. Here's a simple example:

```ruby
module InstanceMethods
  def instance_method
    puts "I'm an instance method!"
  end
end

class MyClass
  include InstanceMethods
end

obj = MyClass.new
obj.instance_method  # Output: "I'm an instance method!"
```

### `module ClassMethods`

There is an e.g. of this spell in the Rails source: `gems/activerecord-2.3.2/lib/active_record/validations.rb`...

Ruby doesn’t have a native way to add class methods through a module directly. However, a common pattern is to define a nested `ClassMethods` module within the main module. This nested module contains methods that are intended to be class methods. Then, you use the `included` hook to extend those methods onto the class itself. Here's an example:

```ruby
module MyModule
  def self.included(base)
    base.extend(ClassMethods)
  end
  
  module ClassMethods
    def class_method
      puts "I'm a class method!"
    end
  end

  def instance_method
    puts "I'm an instance method!"
  end
end

class MyClass
  include MyModule
end

MyClass.class_method  # Output: "I'm a class method!"
obj = MyClass.new
obj.instance_method   # Output: "I'm an instance method!"
```

In this example, `MyClass` gets both the instance methods from `MyModule` and the class methods from `MyModule::ClassMethods`.

### Why Use This Pattern?

This pattern allows you to encapsulate both instance-level and class-level behavior in a single module. This is useful for DRYing up your code and for creating reusable components that can easily be mixed into classes to augment their behavior with both instance and class methods.
