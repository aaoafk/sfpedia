---
title:      "open class"
date:       2023-08-31T08:14:42-04:00
tags:       ["git", "metaprogramming", "ruby"]
identifier: "20230831T081442"
---

in ruby we can re-open class definitions and overwrite methods on the class. How do we do this?

```ruby
class Foo
  def bar
	  'in bar'
  end
end

class Foo
  def bar
	  'hoge'
	end
end

x = Foo.new
x.bar # => 'hoge'
```

Doing this on a core class is known as monkeypatching.