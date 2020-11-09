---
layout: page
title: React Setup
permalink: /new-react/
---

# With Rails 6

## React on Rails App or Add to Existing

### Existing App

If your app is already up:
`rails webpacker:install:react`
This installs all of the babel and webpack dependencies along with react and react-dom.

### New App

`rails new <name> -d-postgresql --webpack=react`

## Add additional needs

`yarn add react-router-dom react-redux redux redux-logger redux-thunk`
This gives us tooling to use redux, create app routes for the user to see, and a couple middlewares.

## Set Up Folders

Assets now live in the `app/javascript` (singular!) directory alongside packs and channels. `application.js` can be used as the entry file for rendering into the dom and place components and store folders alongside.

```
cd app/javascript && mkdir actions components reducers store util && cd .. ..
```

The folder should now look something like this

```
app/javascript
  + actions
  + channels
   - (may have system files)
  + components
  + packs
    - application.js
  + reducers
  + store
  + util
```

## Serve up a static page

Rails might as well serve up your static page, although this not necessarily need be the case. For now though:

### Create a static pages controller

`rails g controller StaticPages`

### Add controller action and view

I prefer to use a custom root view, but index can work too. No need to put anything inside, it will find the corresponding view.

Add to the new controller

```ru
// app/controllers/static_pages_controller.rb
 def root
 end
```

Add a view for it to use

```js
// app/views/static_pages/root.html.erb
<div id="root">Rails</div>
```

### Check it

Run `rails s` and make sure you get plain text Rails on the localhost.
