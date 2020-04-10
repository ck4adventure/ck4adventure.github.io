# ck4adventure.github.io

> Page Under Construction - List of Tools Below

## Homebrew
#### Update:

`brew update`

NB: this now auto runs before any install

## rbenv
#### Upgrade:
`brew upgrade rbenv ruby-build`

#### Check:
`curl -fsSL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-doctor | bash`

#### Install Ruby:
`rbenv install x.y.z`

Currently using 2.6.6 (Apr 7, 2020, aware of 2.7)

#### Use Version Global
`rbenv global x.y.z`

##### Use Version Local
`rbenv local x.y.x`

#### Check ruby version
`ruby -v`

#### Install Bundler
`gem install bundler`

## Rails
Rails 6 Apr 2020

#### Install
`gem install rails`

## Postgresql
#### Install
`gem install pg`

#### Install App
Download postgresapp and run

## Node

#### Install and Use Version
`nvm install x.y.z`

#### Set an alias
`nvm alias <name> <version>`

## Yarn
`brew install yarn`

## New Project
`rails new <name> --database=<db>`
`rails new <name> -d <db>`

Using `postgresql` (Apr 7, 2020)

`rake db:create` to ensure you have your db connections working

## Gemfile
gemfile - best practice is to set specific versions only
`pry-rails` - is what gives us rails console
add into file

then
`bundle install` to update the gemfile lock

`/app`
model is the class that represents the table of the db
controller handles the data coming, accesing the models, and then the views to provide a response
view is a template for the data to be presented for return

/config
database.yml
specifies which db and how it connects
routes.rb
defines what http routes are avail and which controllers to create and trigger actions on

/db
seeds.rb
holds the test data

/lib
holds any classes me made internally

/public
404 pages
custom html stuff
/test

/vendor
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
class Cat < ActiveRecord

end

rails c

able to call the cat class
c = Cat.new
makes a local instance in the rails console without saving to db until you ask for save
c.name = "Sarah"
c.save

read cat from the db
Cat.first