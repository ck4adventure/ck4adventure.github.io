---
layout: page
title: Rails Models
permalink: /rails-models/
---

## Models and Migrations

### Create Model
`rails g model SingularItemName`

#### For minor changes and updates to a model
`rails g migration NameOfChange`

### Add table cols and indexes
```ru
# /db/migrate/20200701_create_users.rb
def change
  # commands run in here
  create_table :users do |t|
    t.string :email, null: false
    t.boolean :marketing, null: false, default: true
    t.timestamps
  end

  # indexes, indiv line changes happen down here
  add_index :users, :email, unique: true
  # can access any existing table too
  add_column :cats, :color, :string
end
```

### Run migrate which annotates all the things
`rake db:migrate`

#### Doesn't quite work yet?
`rails db:rollback` - will undo the last migration

NB: won't work in production env





