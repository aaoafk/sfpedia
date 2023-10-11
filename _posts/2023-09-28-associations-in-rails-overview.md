---
title:      "associations in rails overview"
date:       2023-09-28T09:23:56-04:00
tags:       ["associations", "rails"]
identifier: "20230928T092356"
---

An *association* is a connection between two *active record models*.
We need *associations* between *models* because they simplify
database related operations.

Without *associations* code can be more complex, meditate on the
following e.g.

```ruby
class Author < ApplicationRecord; end;
class Book < ApplicationRecord; end;

# => Associate a book with an author

book = Book.create published_at: Time.now, author: @author.id, title:
"Foo"

# => Destroy all books by an author

@books = Book.where author_id: @author.id
@books.each do |book|
  if book.author_id = @author.id
    book.destroy
  end
end

@author.destroy
```

*Associations* let us streamline some of these operations:

```ruby
class Author < ApplicationRecord
  has_many :books, dependent: destroy
end

class Book < ApplicationRecord
  belongs_to :author
end
```

With that change creating a book for an author is easier:

```ruby
@book = @author.books.create published_at: Time.now
```

This deletes an author **and** all of its books.

```ruby
@author.destroy
```


