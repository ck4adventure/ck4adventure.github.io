---
layout: page
title: Rails Setup
permalink: /new-rails/
---

## New Rails Project

### Traditional App w/ Views
`rails new <name> --database=<db>`

### PG / Rails 6 / RSpec / React

#### Set db to postgres 
`-d=postgresql`

#### Skip default testing 
`-T` 

#### Preconfigure for React
`--webpack=react`

#### Skip the coffee script scss
`--skip-coffee`

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
  # if going old school RoR controller testing
  gem 'rails-controller-testing'
end
```

### Install new gems

Run `bundle install`

### Install rspec testing

Run `rails g rspec:install`

### Install Shoulda Matchers

Place this at the bottom of `spec/rails_helper.rb`:

```ru
Shoulda::Matchers.configure do |config|
  config.integrate do |with|
    with.test_framework :minitest
    with.library :rails
  end
end
```

### Install cucumber bdd

Run `rails g cucumber:install`

### Install annotate gem
This will set annotate to run automatically and with nicer data
Run `rails g annotate:install`

### Configure Factory Bot Rails
If you're using Rails, add the following configuration to `spec/support/factory_bot.rb` and be sure to require that file in `rails_helper.rb`:

```ru
RSpec.configure do |config|
  config.include FactoryBot::Syntax::Methods
end
```

NB: Or you can paste the whole thing in the bottom of the `rails_helper.rb` ala shoulda-matchers config.


## Setup DB

### Postgresql

Make sure it's up and running

### Create the project db

Doing this first can help make sure no errors and connected
`rails db:create`