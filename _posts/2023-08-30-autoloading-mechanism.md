---
title:      "autoloading mechanism"
date:       2023-08-30T23:19:52-04:00
tags:       ["metaprogramming", "rails", "ruby"]
identifier: "20230830T231952"
---

`autoload` is used a lot in Rails. `autoloading` is a way to
automagically `require` a piece of code just when its needed. It's a
class method that is defined by `ActiveSupport::Autoload` module. It
relies on a naming convention to automatically detect the code that it
needs to load. 

Keep in mind that we can extend `ActiveSupport::Autoload` inside our
modules to eager load conveniences for our library. The library guesses
file paths based on rails conventions, i.e. we don't need to define
them when we `autoload :FeatureName`, it also defines constants that
need to be eager loaded.

`ActiveRecord::Base` module uses this extensively and effectively acts like a smart namespace that will automatically require whatever is needed. Keep in mind that the constants are setup to be loaded this has to be the case for other classes that might `include` without a need to explicitly `require` a file.
