---
title:      "async ruby"
date:       2023-09-05T23:06:12-04:00
tags:       ["ruby"]
identifier: "20230905T230612"
---

Asynchronous processing is doing many things at the same time. The reason we need to process things asynchronously is usually because of the stalling time with Input/Output.

Consider the time that we wait to fetch some data over the wire. If we did not have to wait until the fetching of data finished then we would be free to do other things while we waited and process the data once it all got here. Seems a lot better, right?

The issue is that it's hard to abstract the idea of doing many things at the same time without introducing some other scary concepts, like mutexes and we also have to deal with race conditions.

Do not fear the async though. Ruby has a nice `async` ecosystem between `async`, `async-http`, `falcon`, etc.

The usage is simple just shove operations that might take a long time into an `Async do |task| ... end` block. The block is given a task that can responds to `.async` which is given a code block that might take a long time:

```ruby
Async do |task|
  task.async do
	  sleep(1000)
	end

  task.async do
	  # Fat operation
	end
end
```

Don't forget to `require 'async'` and keep in mind that `async` works with most gems because of its usage of the `FiberScheduler` in ruby.