---
layout: page
title: Rails Setup
permalink: /new-project/
---

## New Rails Project
`rails new <name> --database=<db>`
`rails new <name> -d <db>`

Using `postgresql` (Apr 7, 2020)

## Add Testing and Debugging Gems

### Update the Gemfile
gemfile - best practice is to set specific versions only

```ru
group :development do
  gem 'better_errors'
  gem 'binding_of_caller'
  gem 'annotate' # `annotate --models` for schema luv
end
```
```ru
group :development, :test do
  gem 'rspec-rails' # rspec testing, incls core, etc `rails g install:rspec`
  gem 'pry-rails' # pry instead of irb
  gem 'factory_bot_rails'
  gem 'faker'
end
```
```ru
group :test do
  gem 'guard-rspec' # hot rspec testing
  gem 'launchy' # `Launchy.open(url)`
  gem 'shoulda-matchers' # enables one-liner syntax
end
```

### Install new gems
Run `bundle install`


### Install rspec testing
Run `rails g rspec:install`


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

`/spec`
testing files go here

`/vendor`
js files and libraries from external sources

## Setup DB
### Postgresql
Make sure it's up and running

### Create the project db
Doing this first can help make sure no errors and connected
`rails db:create`


#### TADA! You now have a working rails app with database!

