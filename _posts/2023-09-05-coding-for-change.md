---
title:      "Coding for change"
date:       2023-09-05T10:24:14-04:00
tags:       ["ruby", "softwaredevelopment"]
identifier: "20230905T102414"
---

We should design our code around behavior rather than data.

1. Hide instance variables by wrapping them into a message send to `attr_reader` for e.g.

2. Hide complicated data structures from yourself. Metz explained this by using Ruby `Struct` to give structure to some data. I like this principle because it can apply to data structures that you create which you will inevitably forget the meaning of when done coding or for externally provided data input.

3. Enforce SRP for methods too. This rule is a little more subjective I think? The benefits to coding in this style are, allegedly: expose previously hidden qualities, avoid the need for comments, encourage reuse and are easy to move to another class.

