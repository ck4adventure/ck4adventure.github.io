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

### Add additional needs
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
<div id='root'>Rails</div>
```

### Check it
Run `rails s` and make sure you get plain text Rails on the localhost.

# OLD React Framework on top of Rails Backend

## Check your Node version
Some webpacker packages seem to be unable to upgrade on node
Currently running Node 8.9.4 for Rails 5.2.3, but prolly needs to be pre 5.2

### Init a package file
Add a package file to your project, `--y` will set minimal defaults.

```bash
npm init --y
```

### Install framework packages

```bash
npm install @babel/core @babel/preset-env @babel/preset-react babel-loader react react-dom react-redux react-router-dom redux redux-logger redux-thunk webpack webpack-cli
```
### Add webpack script
In the `package.json` file add the webpack line to the scripts section.

```json
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "postinstall": "webpack",
    "webpack": "webpack --watch --mode=development"
  },
```

### Add webpack config file

In the root directory of the project, add a file `webpack.config.js` with these contents.

```bash
touch webpack.config.js
```

```js
const path = require('path');

module.exports = {
  context: __dirname,
  entry: './frontend/entry.jsx',
  output: {
    path: path.resolve(__dirname, 'app', 'assets', 'javascripts'),
    filename: 'bundle.js'
  },
  resolve: {
    extensions: ['.js', '.jsx', '*']
  },
  module: {
    rules: [
      {
        test: /\.jsx?$/,
        exclude: /(node_modules)/,
        use: {
          loader: 'babel-loader',
          query: {
            presets: ['@babel/env', '@babel/react']
          }
        },
      }
    ]
  },
  devtool: 'source-map'
};

```

## Set up framework file structure

### Add folders
```
mkdir frontend && cd frontend && mkdir actions components reducers store util && cd ..
```
```
frontend
  + actions
  + components
  + reducers
  + store
  + util
```

### Add entry point
```js
// frontend/entry.jsx
import React from 'react';
import ReactDOM from 'react-dom';

document.addEventListener('DOMContentLoaded', () => {
  const rootEl = document.getElementById('root');
  ReactDOM.render(<h1>New App Starts Here</h1>, rootEl);
});
```

### Add index.html
Set div with id=root.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>App Title</title>
</head>
<body>
  <div id="root">oops the app broke</div>
</body>
</html>
```

## Test it

Run `npm run webpack` and open the index.html file in your browser, you should see the welcome message. Debug as necessary.

