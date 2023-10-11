---
title:      "Value Objects"
date:       2023-08-17T08:47:56-04:00
tags:       ["rails", "ruby"]
identifier: "20230817T084756"
---

Value objects are simple objects whose equality is dependent on their
value rather than an identity. They are usually immutable.

In Rails, Value Objects are great when you have an attribute or small
group of attributes that have logic associated with them. Anything
more than basic text fields and counters are candidates for Value
Object Extraction.

Value objects are richer domain objects that replace the use of a
primitive.

There are two high-level "concepts of equality" in Ruby:

1) Equal by identity (objects being compared are the same object in
   memory).

	 2) Equal by value (objects being compared represent the same value)

By default, primitives and structs compare by value while instances of
user-created classes compare by identity. When we create a value
object, we're trying to override the default to compare by value
rather than by identity.

Two value objects that represent the same value should:

1) ~==~ each other
	 2) NOT ~equal?~ each other (~equal?~ should compare by identity,
      not by value)
			3) ~hash~ to the same value (so we don't break hash keys)
				 4) ~eql?~ each other (Ruby expects objects that have the same
            ~hash~ to be ~eql?~ to each other other)


Here's an e.g. implementation:

```ruby
	class Duration
		attr_reader :minutes

		def initialize(minutes)
			@minutes = minutes
		end

		def ==(other)
			minutes == other.minutes
		end

		alias_method :eql?, :==

		def hash
			[self.class, minutes].hash
		end
	end
```

Keep in mind that Ruby structs implement these features by default.

Recall, that Value Objects should be immutable, which means we should
probably freeze in the constructor, and any methods that would modify
the object (e.g. addition) should return a new instance. It could be
nice to implement `<=>` and `include Comparable` that can get you `==`
for free and also allow you to use the value in a range.
