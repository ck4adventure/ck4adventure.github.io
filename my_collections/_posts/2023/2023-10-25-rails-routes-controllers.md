---
layout: page
title: Routes and Controllers
topic: rails
category: rails
---

### Controllers and Routing

A refresher on setting up complex routes and controllers.

#### Removing CSRF Protection for Postman Testing

Add `config.action_controller.default_protect_from_forgery = false` right after `config.load_defaults 5.2` in the `config/application.rb` file

### Routes Examples
```ru
root_to 'mycontroller#index'

resources :users

resources :session, only: [:new, :create, :destroy]

resources :items, except: [:destroy] members do
  resources :weapons, shallow: true
end

resources :weapons, only: [:update, :edit, :create]
```