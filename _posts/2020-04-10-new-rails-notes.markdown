---
layout: post
title:  "Rails Project Crib Notes"
date:   2020-04-10 17:04:08 -0700
categories: rails how-to notes
---

## New Rails Project
`rails new <name> --database=<db>` OR  
`rails new <name> -d <db>`

Using `postgresql` (Apr 7, 2020)

`rake db:create` to ensure you have your db connections working

## Add Addtl Tools to Gemfile
gemfile - best practice is to set specific versions only

```ru
group :development do
  gem 'better_errors'
  gem 'binding_of_caller'
  gem 'pry-rails'
end
```
```ru
group :development, :test do
  gem 'rspec-rails'
  gem 'factory_bot_rails'
end
```
```ru
group :test do
  gem 'faker'
  gem 'guard-rspec'
  gem 'launchy'
end
```

`bundle install` to update the gemfile lock

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

`/lib`
holds any classes made internally

`/public`
404 pages
custom html stuff
/test

`/vendor`
js files and libraries from external sources

## Migrations
Rails writes our sql tables for us
record of the changes of the db

rails generate migration CreateObjectTable - somewhat semantic what you did, to read it, but isn't critical, ruby will try to read it though

creates a .rb file with a timestamp, snakecased
def change
  <commands run in here/>
  create_table :objectplural do |t|
    t.string :name, null: false
    t.timestamps
  end
end


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

class Cat (class and file name should be same, but different case)
class Cat < ApplicationRecord

end

rails c

able to call the cat class
c = Cat.new
makes a local instance in the rails console without saving to db until you ask for save
c.name = "Sarah"
c.save

read cat from the db
Cat.first

#### annotate gem
add to development group
gem 'annotate'

then `bundle install`

then, as long as your model files exist with the class skels
`bundle exec annotate --models`

## Write basic macros for associations
instead of writing out queries, belongs_to and has_many and others are boilerplate ensure functions and checks

belongs_to :model, {
  primary_key: :id,
  foreign_key: :other_id,
  class_name: 'Class'
}

## Complex Asociations
double
has_many :things
  through: <an association>
  source: <method on the association you're accessing that returns the things>
returns an array

has_one :thing
  through: <name of some association>
  source: <method on there that gets you the rest of the way to the thing>
returns single object, uses LIMIT 1

## Basic Validations

It is important to make sure that any entries saved to the db are complete and will not throw any kind of errors when it does try to save. A db level exception will throw a 500 level error up to the user experience, no bueno.

Instead, by ensuring there is a validation set on every piece of information in a meaningful way, errors can be created and sent to ensure the user is able to correct her entry accordingly.

Anything with a `null:false` on the migration should have a `presence:true`

Same for anything that gets a `unique: true` via indexing should validate `uniqueness: true`

Validation    |  Database Constraint  |  Model Validation
-----------   |-----------------------|------------------
Present       |  null: false          |  presence: true
All Unique    |  add_index :tbl, :col, unique: true                   | uniqueness: true
Scoped Unique |  add_index :tbl, [:scoped_to_col, :col], unique: true | uniqueness: { scope: :scoped_to_col }

Also:
* `format`
    * Tests whether a string matches a given regular expression
* `length`
    * Tests whether a string or array has an appropriate length. Has
      options for `minimum` and `maximum`.
* `numericality`; options include:
    * `greater_than`/`greater_than_or_equal_to`
    * `less_than`/`less_than_or_equal_to`
* `inclusion`
    * `in` option lets you specify an array of possible values. All
      other values are invalid.

Caveat!
Rails 5 automatically validates the presence of `belongs_to` associations.
Use `optional: true` to the association initialization to remove presence requirement.
Don't double up with an extra validates presence at the top either, leads to confusing messages.

#### Custom Vals
It is super easy to write a custom method for validation:

```ruby
class Invoice < ApplicationRecord
  # validate tells the class to run these methods at validation time.
  validate :method_that_checks_something

  private
  def method_that_checks_something
    if something.false
      errors[:object] << 'semantic description of error goes here.'
    end
  end
end
```

Errors :base for when you have no other option:

```ruby
def a_method_used_for_validation_purposes
  errors[:base] << 'This person is invalid because ...'
end
```

#### Testing in the Console

Create a new object, such as 
`j = User.new`
`j.valid?` Will return false if any error messages in the array, true if clean.

To get an array of the human readable messages (such as you made above), call `<record>.errors.full_messages`. Remember, it only fails if a message gets put in.