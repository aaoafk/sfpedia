---
title:      "Forwardable"
date:       2023-08-24T18:26:35-04:00
tags:       ["ruby"]
identifier: "20230824T182635"
---

Delegation is just the forwarding of messages.

In Ruby, `Forwardable` provides delegation of specific messages to an object,
using the methods `def_delegator` and `def_delegators`.

E.g. if we have a class ~RecordCollection~ with an ~@records~ instance
variable, that we know is an array, and we want to provide a method
like ~record_count~ on ~RecordCollection~ we can do this:

```ruby
class RecordCollection
	include Forwardable

    # => Instance variable @records set maybe in the initialize
    method?
    ...
    # => record_count is accepted but it'll just exec []
	def_delegator :@records, :[], :record_count
	
	# => delegate a bunch of messages
	def_delegators :@records, :push, :shift, ...
end
```


~Forwardable~ is about individual messages while ~Delegator~ is the
whole inbox...
