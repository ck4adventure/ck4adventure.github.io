---
layout: page
title: Routes and Controllers
permalink: /rails-controllers/
---

### Controllers and Routing
A refresher on setting up complex routes and controllers.

#### Removing CSRF Protection for Postman Testing
Add `config.action_controller.default_protect_from_forgery = false` right after `config.load_defaults 5.2` in the `config/application.rb` file