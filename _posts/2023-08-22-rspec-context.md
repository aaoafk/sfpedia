---
title:      "rspec context"
date:       2023-08-22T16:12:06-04:00
tags:       ["rspec"]
identifier: "20230822T161206"
---

title:      rspec context
date:       2023-08-22
tags:       rspec
identifier: 20230822T161206
---------------------------

rspec also provides ~context~ block which is just an alias for
~describe~ it provides a different way to express ourselves.

~context~ is used for phrases that modify the object that we're
testing.

```ruby
    RSpec.describe "Coffee" do
        let(:coffee) { Coffee.new :black }
        context "with milk" do
            it "has milk" do
                expect(coffee.has_milk?).to eq(false)
            end
        end
    end
```
