---
title:      "Rails environments"
date:       2023-08-16T13:44:25-04:00
tags:       ["rails"]
identifier: "20230816T134425"
---

All Rails applications come with three environments out of the box:
development, test and production. We can always add more like:
staging, QA, etc.

All Rails configuration files live under the ~config~ directory.
~bin/rails about~ gives us a snapshot of the state of our Rails
application--or ~bundle exec rails about~ if you want to execute it
within the context of our Bundler file. It lists various version
information like the Rails version, ruby version, rack version,
middleware, etc.

We can specify the current environment using ~RAILS_ENV~ variable.
It's value is set to one of the files under ~config/environments~ we
could also create a _staging.rb_ file and set ~RAILS_ENV~ to
`staging`. We create new environments by just creating a new file with
the environment name.

If ~RAILS_ENV~ is not set then Rails will check ~RACK_ENV~ to figure
out the environment, if ~RACK_ENV~ is not set then the environment is
`development` by default.

We can figure out the current environment programatically with
~Rails.env~ value. Rails also has helpers like ~Rails.env.production?~
and ~Rails.env.development?~

We can scope gems to an environment in our _Gemfile_ with a ~group
:env_name do end~ block, e.g. ~group :test do gem "foobar" end~.

Shared configuration between environments is added in
~config/application.rb~. Of course, configuration in
~config/environments/*.rb~ is evaluated last and that is what has the
final say in what our configuration looks like.

The `db:environment:set` task doesn't change the current environment
Rails is running in. Instead, it sets the environment information in
the `ar_internal_metadata` table. The purpose of this is to protect
your database by storing what environment it's intended for. For
instance, it can prevent you from mistakenly running destructive
commands on your production database thinking it's a development
database. 

The `Rails.env` method, on the other hand, returns the current
environment your Rails application is running in. This is typically
determined by the `RAILS_ENV` environment variable or falls back to
"development" if that variable isn't set.

Here's how you can switch and check environments:

1. **Switching Environments Using `RAILS_ENV`**:
   
   To run a task in a specific environment, you'd prefix your command with the `RAILS_ENV` variable:

   ```bash
   RAILS_ENV=test bundle exec rails console
   ```

   In the above command, you're starting the Rails console in the test environment.

2. **Checking the Current Environment**:

   Once inside the console, you can verify the current environment with:

   ```ruby
   Rails.env
   ```

   This should return `test` if you started the console with `RAILS_ENV=test`.

3. **Remember `RAILS_ENV` is Temporary for that Command**:

   Setting `RAILS_ENV` before a command does not persistently change
   the environment your Rails application uses. It only applies for
   the duration of that command.  

If you consistently want to change the environment your application
runs in without always specifying `RAILS_ENV`, you'd typically adjust
environment configurations outside of Rails, such as in your
deployment setup, application server configuration, or shell profile.  

However, in a development context, it's more common to switch
environments on-the-fly using the `RAILS_ENV` variable as shown above. 
