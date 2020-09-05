---
layout: page
title: Rails Setup
permalink: /new-rails/
---

## New Rails Project

`rails new <name> --database=<db>`

`rails new <name> -d <db>`

Using `postgresql` (Apr 7, 2020)

## Add BDD and testing gems

### Update the Gemfile

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
group :development do
  # personal dev gems
  gem 'better_errors'
  gem 'binding_of_caller'
  # `annotate --models` for schema luv
  gem 'annotate'
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
  # cucumber for end to end testing
  gem 'cucumber-rails', require: false
  # database cleaner to keep it squeakin
  gem 'database_cleaner'
end
```

### Install new gems

Run `bundle install`

### Configure Auto-Generation of RSpecs

Add inside the Application Class in the file '<app>/config/application.rb'

```ru
config.generators do |g|
  g.test_framework :rspec,
    :fixtures => true,
    :view_specs => false,
    :helper_specs => false,
    :routing_specs => false,
    :controller_specs => true,
    :request_specs => false
end
```

### Install Shoulda Matchers

Place this at the bottom of `test/test_helper.rb`:

```ru
Shoulda::Matchers.configure do |config|
  config.integrate do |with|
    with.test_framework :minitest
    with.library :rails
  end
end
```

## Setup DB

### Postgresql

Make sure it's up and running

### Create the project db

Doing this first can help make sure no errors and connected
`rails db:create`

### Install rspec testing

Run `rails g rspec:install`

### Install cucumber bdd

Run `rails g cucumber:install`
