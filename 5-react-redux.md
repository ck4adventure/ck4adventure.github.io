---
layout: page
title: React-Redux
permalink: /react-redux/
---
# Wiring in the Framework

## Entry File
With Rails and Webpacker, `application.js` is what Rails knows to look for and will compile into packs. 

Here React and React DOM combine to render the root element into the html tag given. In the initial setup, a placeholder element is put in to verify js is compiling correctly and also finding the DOM element.

Later, it will configure a store with any preloaded state needed and pass that to a component called Root, which in turn can wrap more components.

```js
// app/javascript/packs/application.js
// below the other requires
import React from 'react';
import ReactDOM from 'react-dom';

//import configureStore from './store/store';
//import Root from './components/root';


document.addEventListener('DOMContentLoaded', () => {
  //const store = configureStore();
  //const root = document.getElementById('root');
  // ReactDOM.render(<Root store={store} />, root);
  ReactDOM.render(<h2>React App!</h2>, root);
});
```

## Check it
Start the webpacker in watch mode, since you'll need it in a few.
`./bin/webpack --watch --colors --progress`

Make sure `React App` is now the text appearing on the page.

## Root Component
The Root component is single use to configure a store Provider for the Redux loop. This allows props to be passed through the 'connect' function when creating individual components.

```js
import React from 'react'
import Provider from 'react-redux'

const Root = ({store}) => (
  <Provider store={store} >
    <h1>Welcome from Provider</h1>
  </Provider>
)

export default Root;
```


### Actions


## Reducers

## Store

## Wrap Provider and Hash Router

## First Component Container
import connect
import actions and selectors
mapStateToProps
mapDispatchToProps
export line

## First Component
Functional Components



## Links and Routes