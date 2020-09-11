---
layout: page
title: Rails Models
permalink: /rails-models/
---



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


