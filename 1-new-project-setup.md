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
  # personal dev gems
  gem 'better_errors'
  gem 'binding_of_caller'
  # `annotate --models` for schema luv
  gem 'annotate'
end
```

```ru
group :development, :test do
  # personal dev gems
  # rspec testing, incls core, etc `rails g install:rspec`
  gem 'rspec-rails'
  # pry instead of irb
  gem 'pry-rails'
  # seed and test data generation
  gem 'factory_bot_rails'

end
```

```ru
group :test do
  # personal dev gems
  # capaybara should come standard now
  # gem 'capybara'
  # hot rspec testing
  gem 'guard-rspec'
  # `Launchy.open(url)`
  gem 'launchy'
  # enables one-liner syntax
  gem 'shoulda-matchers'
  # faker data to work with factory bot
  gem 'faker'
end
```

### Install new gems

Run `bundle install`

### Install rspec testing

Run `rails g rspec:install`

### Configure Auto-Generation of RSpecs

Add inside the Application Class in the file '<app>/config/application.rb'

```ru
config.generators do |g|
  g.test_framework :rspec,
    :fixtures => false,
    :view_specs => false,
    :helper_specs => false,
    :routing_specs => false,
    :controller_specs => true,
    :request_specs => false
end
```

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
