---
layout: page
title: Older React Setup
topic: rails
---

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
const path = require("path");

module.exports = {
  context: __dirname,
  entry: "./frontend/entry.jsx",
  output: {
    path: path.resolve(__dirname, "app", "assets", "javascripts"),
    filename: "bundle.js",
  },
  resolve: {
    extensions: [".js", ".jsx", "*"],
  },
  module: {
    rules: [
      {
        test: /\.jsx?$/,
        exclude: /(node_modules)/,
        use: {
          loader: "babel-loader",
          query: {
            presets: ["@babel/env", "@babel/react"],
          },
        },
      },
    ],
  },
  devtool: "source-map",
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
import React from "react";
import ReactDOM from "react-dom";

document.addEventListener("DOMContentLoaded", () => {
  const rootEl = document.getElementById("root");
  ReactDOM.render(<h1>New App Starts Here</h1>, rootEl);
});
```

### Add index.html

Set div with id=root.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>App Title</title>
  </head>
  <body>
    <div id="root">oops the app broke</div>
  </body>
</html>
```

## Test it

Run `npm run webpack` and open the index.html file in your browser, you should see the welcome message. Debug as necessary.
