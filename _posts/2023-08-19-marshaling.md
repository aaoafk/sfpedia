---
title:      "marshaling"
date:       2023-08-19T16:32:54-04:00
tags:       ["ruby", "serialization"]
identifier: "20230819T163254"
---

title:      marshaling
date:       2023-08-19
tags:       ruby  serialization
identifier: 20230819T163254
---------------------------

In computer programming, this process of serialization and
deserialization of an object is what we commonly call object
marshalling.

`marshaling` is the process of converting an object or data structure
into a format that can be easily stored or transmitted and then
reconstructed later.  It's just a way to serialize and deserialize
objects.

Ruby provides the ~Marshal~ library to do this:

* Not every object can be marshaled if we try to marshal unsupported objects then we get a ~TypeError~

* Marshaled data is tightly coupled to the ruby version

* Don't unmarshal data from untrusted sources because this can lead to arbitrary code execution.

Rails developers prefer to use more portable serialization formats
like JSON or MessagePack, which aren't tied to Ruby's specific data
structures and types. 

There are two methods of doing this, your object can define either
marshal_dump and marshal_load or _dump and _load. marshal_dump will
take precedence over _dump if both are defined. marshal_dump may
result in smaller Marshal strings.

* _dump and _load are more nuanced than marshal_load or marshal_dump...

** _dump requires you to return a string that represents the data to serialize
** we're in charge of knowing the structure of the string

** _load accepts the serialized string as an argument and we need to instantiate
** the object ourselves
