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

## Using Models to interact with the db

Models as object oriented ways to interact
cat.rb to model the cats table

```ru
class Cat (class and file name should be same, but different case)
class Cat < ApplicationRecord

end
```

`rails c`

able to call the cat class
`c = Cat.new`
makes a local instance in the rails console without saving to db until you ask for save
`c.name = "Sarah"`
`c.save`

read cat from the db
`Cat.first`

### Annotate Gem

as long as your model files exist with the class skels
`bundle exec annotate --models` (--routes, --controllers, etc)

## Write basic macros for associations

instead of writing out queries, belongs_to and has_many and others are boilerplate ensure functions and checks

```ru
belongs_to :model, {
  primary_key: :id,
  foreign_key: :other_id,
  class_name: 'Class'
}
```

## Complex Asociations

double

```ru
has_many :things
  through: <an association>
  source: <method on the association you're accessing that returns the things>
```

returns an array

```ru
has_one :thing
  through: <name of some association>
  source: <method on there that gets you the rest of the way to the thing>
```

returns single object, uses LIMIT 1
