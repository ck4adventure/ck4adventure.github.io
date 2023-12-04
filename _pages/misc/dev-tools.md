---
layout: page
title: Dev Tools
permalink: /dev-tools
---
# Managing Environments

## Python
`venv` [Python Virtual Environment](https://docs.python.org/3/library/venv.html)
Create base folder for project: use system python3 to create a base virtual env for python development `python3 -m venv venv`

Activate: `source venv/bin/activate`

Deactivate: from within active env, `deactivate`

## Node
`nvm` [Node Version Manager](https://github.com/nvm-sh/nvm)
Use an .nvmrc file to store the version of node the project should use
Can either remember to run `nvm use` when switching into project or find an auto-switch solution such as `avn`

Install and Use Version: `nvm install x.y.z`

Use Version: `nvm use lts/iron` or `nvm use default` or `nvm use x.y.z`

Set an alias: `nvm alias <name> <version>`

## Ruby
`rbenv` [Ruby Environments](https://github.com/rbenv/rbenv)

Install: `brew install rbenv ruby-build`

Upgrade: `brew upgrade rbenv ruby-build`

Check: `curl -fsSL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-doctor | bash`

Install Ruby: `rbenv install x.y.z`

Currently using 2.6.6 (Apr 7, 2020, aware of 2.7)

Set global default version: `rbenv global x.y.z`

Set local version: `rbenv local x.y.x`

Check ruby version: `ruby -v`


# Tools

## Homebrew

Update: `brew update`

NB: this now auto runs before any install

## Yarn

`brew install yarn`


# Frameworks

## Jekyll

`brew install jekyll`

## Django
Assuming active venv
Install: `python -m pip install Django`


## Rails
Assuming rbenv set to desired version.
Install Bundler: `gem install bundler`

Install Rails: `gem install rails`

Install PG database connector: `gem install pg`

## PostgreSQL

Download postgresapp and run



