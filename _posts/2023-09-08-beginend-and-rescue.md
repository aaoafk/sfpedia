---
title:      "begin/end and rescue"
date:       2023-09-08T22:24:12-04:00
tags:       ["ruby"]
identifier: "20230908T222412"
---

The beginning of a method or code block provides an implicit begin/end context. Therefore, if we use `rescue` keyword inside a method or code block, you don't have to say begin explicitly-assuming that we want the `rescue` clause to govern the entire method or block:

Meditate on the following example:

```ruby
def open_user_file
  File.open 1
	rescue Exception => e
	  puts "#{e.msg}"
end