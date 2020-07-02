---
layout: page
title: DB and Models
permalink: /rails-models/
---
## Migrations
Rails writes our sql tables for us
record of the changes of the db

`rails generate migration CreateObjectTable` - somewhat semantic what you did, to read it, but isn't critical, ruby will try to read it though

creates a .rb file with a timestamp, snakecased
```ru
def change
  <commands run in here/>
  create_table :objectplural do |t|
    t.string :name, null: false
    t.timestamps
  end
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