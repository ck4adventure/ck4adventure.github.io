---
layout: page
title: Rails DB
permalink: /rails-models/
---

## Tour the App Structure

`/app`
model is the class that represents the table of the db
controller handles the data coming, accesing the models, and then the views to provide a response
view is a template for the data to be presented for return

`/config`
database.yml
specifies which db and how it connects
routes.rb
defines what http routes are avail and which controllers to create and trigger actions on

`/db`
seeds.rb
holds the test data

`/features`
holds cucumber bdd feature files and their steps

- A cucumber file is named `<feature_desc>.feature` and lives at the top level

- `/features/step_definitions` holds the steps to be tested
- `/features/support` holds support files like the env

`/lib`
holds any classes/files made internally

`/public`
404 pages
custom html stuff

`/spec`
testing files go here

- '/spec/factories' Factory Bot files
- '/spec/models' RSpec model tests
- '/spec/controllers' RSpec controller tests

`/vendor`
js files and libraries from external sources

## Models and Migrations

Rails writes our sql tables for us using ActiveRecord. It also keeps a record of the changes of the db through migrations.

`rails generate migration CreateUsers`

- try to use a semantic naming, rails will try to parse
- migrations will create a table if nonexistent

creates a .rb file with a timestamp, snakecased

```ru
# /db/migrate/20200701_create_users.rb
def change
  # commands run in here
  create_table :users do |t|
    t.string :email, null: false
    t.timestamps
  end

  # indexes, indiv line changes happen down here
  add_index :users, :email, unique: true
end
```

then:
`rake db:migrate`, which executes any code in the change method

to check the state the db is in, need to check the schema
schema.rb

`rails g migration CreateToys`

to rollback the last
`rake db:rollback` - should work on standard things, but usually you need the on down methods within the migration to handle it more finely

don't rollback in production, only forward edits, like git has to

to add a column, within the change code of a migration:
`add_column :cats, :color, :string`


