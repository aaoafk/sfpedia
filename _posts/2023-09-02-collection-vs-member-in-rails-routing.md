---
title:      "collection vs member in rails routing"
date:       2023-09-02T13:21:00-04:00
tags:       ["rails", "routing"]
identifier: "20230902T132100"
---

```ruby
resources :photos do
  member do
    get :preview
  end
end

vs.

```ruby
resources :photos do
  collection do
    get :search
  end
end

A member route will require an ID, because it acts on a member. A collection route doesn't because it acts on a collection of objects. Preview is an example of a member route, because it acts on (and displays) a single object. Search is an example of a collection route, because it acts on (and displays) a collection of objects.

THE FULL EXPLANATION:

The `collection` block in the `routes.rb` file is a way to specify routes that act on a collection of resources as opposed to a single resource. In RESTful terms, actions within the `collection` block don't necessarily pertain to a single, specific resource instance identified by an ID. 

In a standard `resources` declaration, Rails assumes that you're going to be acting on individual records, so it provides routes like `/totps/:id` (where `:id` is the ID of a specific `totp`). 

But when you're dealing with actions like enabling, disabling, or verifying TOTP, these actions don't necessarily act on a specific "record" in the way that updating or deleting would. They act on the general concept of TOTP for a user. 

Here's a breakdown for clarity:

- Standard REST actions (`index`, `show`, `new`, `create`, `edit`, `update`, `destroy`) usually act on either a single resource instance (`:id` is present in the URL) or the entire collection of resources (no `:id` in the URL).
  
- `collection` actions always act on the collection itself and not on individual records. In this case, enabling TOTP isn't about changing a specific TOTP record, but rather about affecting the user's general ability to use TOTP as a feature.

By placing these custom actions (`enable`, `disable`, `verify`, `setup`) within the `collection` block, you're specifying that these routes should be generated without the need for an `:id` parameter in the URL. Therefore, you'll get routes like `/totp/enable` instead of `/totp/:id/enable`.