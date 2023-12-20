---
layout: page
title: React Setup
topic: rails
---

# With Rails 6

## React on Rails App or Add to Existing

### Existing App

If your app is already up:
`rails webpacker:install:react`
This installs all of the babel and webpack dependencies along with react and react-dom.

### New App

`rails new <name> -d-postgresql --webpack=react`

#### Options List
```
      [--skip-gemfile], [--no-skip-gemfile]                  # Don't create a Gemfile
  -G, [--skip-git], [--no-skip-git]                          # Skip .gitignore file
      [--skip-keeps], [--no-skip-keeps]                      # Skip source control .keep files
  -M, [--skip-action-mailer], [--no-skip-action-mailer]      # Skip Action Mailer files
      [--skip-action-mailbox], [--no-skip-action-mailbox]    # Skip Action Mailbox gem
      [--skip-action-text], [--no-skip-action-text]          # Skip Action Text gem
  -O, [--skip-active-record], [--no-skip-active-record]      # Skip Active Record files
      [--skip-active-job], [--no-skip-active-job]            # Skip Active Job
      [--skip-active-storage], [--no-skip-active-storage]    # Skip Active Storage files
  -P, [--skip-puma], [--no-skip-puma]                        # Skip Puma related files
  -C, [--skip-action-cable], [--no-skip-action-cable]        # Skip Action Cable files
  -S, [--skip-sprockets], [--no-skip-sprockets]              # Skip Sprockets files
      [--skip-spring], [--no-skip-spring]                    # Don't install Spring application preloader
      [--skip-listen], [--no-skip-listen]                    # Don't generate configuration that depends on the listen gem
  -J, [--skip-javascript], [--no-skip-javascript]            # Skip JavaScript files
      [--skip-turbolinks], [--no-skip-turbolinks]            # Skip turbolinks gem
      [--skip-jbuilder], [--no-skip-jbuilder]                # Skip jbuilder gem
  -T, [--skip-test], [--no-skip-test]                        # Skip test files
      [--skip-system-test], [--no-skip-system-test]          # Skip system test files
      [--skip-bootsnap], [--no-skip-bootsnap]                # Skip bootsnap gem
```


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
