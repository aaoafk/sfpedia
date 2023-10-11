---
title:      "Rails Routing"
date:       2023-08-18T08:48:19-04:00
tags:       ["rails", "routing"]
identifier: "20230818T084819"
---

* Always use canonical routes that conform to Rails default.

* Never configure a route in ~config/routes.rb~ that is not being used.

* User-friendly URLs should be stapled onto canonical routes.

* Avoid custom actions in favor of creating new resources that use Rails' default actions

* Be wary of nested routes.

Routing is all about matching an HTTP request to a Controller#action.
Routes live in ~config/routes.rb~. Since routing is all about HTTP
requests and HTTP is resource-based supporting a limited amount of
actions we should avoid custom actions whenever possible and start
thinking in terms of resources.

"Controllers are the boundary between HTTP and whatever makes your app
special. Sticking with a resource-based approach with standard actions
for routes and controllers reinforces that boundary and keeps your
app’s complexity out of the controllers."

`Rails.application.routes.draw do ... end` block that wraps your
routes definitions are required to establish the scope for the router
DSL.

`resources` is the rails default and quickly creates necessary routes
for: `index`, `show`, `new`, `edit`, `create`, `update`, and `destroy`
actions.

Browswer requests pages from Rails by making a request for a `URL` using
a HTTP method, such as GET, POST, PATCH, PUT, and DELETE. Each HTTP
method is a request to perform an action in a controller.

There is a concept of singular resources that allow us to map singular
resources to plural controllers, e.g. ~resource :photo~ and
~resources :photos~ creates both singular and plural routes that map
to the same controller ~PhotosController~.

`namespace :SYMBOL_NAME do ... end` allows us to group controllers
under a namespace, e.g.

```ruby
    namespace :admin do
        resources :articles, :comments
    end
```

Leads to the following routes ->

GET -> /admin/articles -> admin/articles#index -> admin_articles_path...

If instead you want to routes `/articles` (without the prefix
`/admin`) to `Admin::ArticlesController`, you can specify the module
with a `scope` block:

```ruby
    scope module: 'admin' do
        resources :articles, :comments
    end
```

`resources` can be nested but...

> `resources` should never be nested more than 1 level deep.

A collection may need to be scoped by its parent, but a specific
member can always be accessed directly by an id, and shouldn't need
scoping (unless the id is not unique, for whatever reason).

`Singular` and `plural` matter a lot. Recall that you can always use
the `resolve` macro to customize which URL and Path helpers that
`Rails` will use when it encounters an instance of a resource. This is
relevant for cases where we might have a resource that we declare
_singularly_:

```ruby
resources :geocoder 

# => Without this line rails would try to find `geocoders` resource
# => With this line we get the correct mapping for an instance of
# => `Geocoder` mapping to the resource `geocoder`
resolve(Geocoder) { [:geocoder] }
```
