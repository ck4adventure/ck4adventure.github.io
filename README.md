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

#### Install
`gem install rails`

## Postgresql
#### Install
`gem install pg`

#### Install App
Download postgresapp and run

## New Project
`rails new <name> --database=<db>`

Using `postgresql` (Apr 7, 2020)

## Node

#### Install and Use Version
`nvm install x.y.z`

#### Set an alias
`nvm alias <name> <version>`

## Yarn
`brew install yarn`