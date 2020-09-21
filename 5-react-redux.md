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
  const root = document.getElementById('root');
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
Exporting a defined constant ensures action types don't fail to typos. Each payload identifies itself by type and delivers all or part of what it received.

```js
export const RECEIVE_ITEMS = "RECEIVE_ITEMS";

export const receiveItems = items => {
  type: RECEIVE_ITEMS,
  items
}
```

## Reducers
Import the actions, create some initial state for testing, and use a switch inside the reducer to handle action types.
Freezing state is important, as is proper merging into a new hash when receiving additional information.

```js
import {RECEIVE_ITEMS} from '../actions/items_actions';

const initialState = {
    1: {
      id: 1,
      name: "Mighty Tester",
      item_type: "weapon",
    },
    2: {
      id: 2,
      name: "Best Base",
      item_type: "base",
    }
};

const itemsReducer = (state = initialState, action) => {
  Object.freeze(state);
  let nextState = {};
  switch (action.type) {
    // currently, replace all on receive
    case RECEIVE_ITEMS:
      action.items.forEach(item => {
        nextState[item.id] = item
      });
      return nextState;
    default:
      return state;
  }
};

export default itemsReducer;
```

## Root Reducer
Although a store can be created from a single function to control state, the reducers allow for controlling smaller slices of state as the app grows. Combining the reducers into a single merged store happens through redux. Import each reducer and add to the "list".

```js
import { combineReducers } from 'redux';

import itemsReducer from './items_reducer';

const rootReducer = combineReducers({
  items: itemsReducer,
});

export default rootReducer;
```

## Store
A store can be very simple, or configured to handle additional needs. Here, allowance is made for an optional preloaded state to be passed in on creation.

```js
import { createStore } from 'redux';

import rootReducer from '../reducers/root_reducer';

const configureStore = (preloadedState = {}) => {
  return createStore(rootReducer, preloadedState);
};

export default configureStore;
```

## Tie it all together
Back in `application.js`, import the configureStore and then invoke it within your document function to trigger the createStore loaded in. 

```js
// app/javascript/packs/application.js
// below the other requires
import React from 'react';
import ReactDOM from 'react-dom';

import configureStore from './store/store';
import Root from './components/root';


document.addEventListener('DOMContentLoaded', () => {
  // pass in any preloaded state here, such as from local storage
  const store = configureStore();
  const root = document.getElementById('root');
  ReactDOM.render(<Root store={store} />, root);
});
```
## Check it
### React setup!
Run webpack if it isn't still watching, and start the rails server if not on. 

The message should change to 'Welcome from Provider'.

### Redux Store!
Test the store by pinning it to the window. (as always, remember to take it back off for prod)

```js
...
// inside eventlistener block
  window.store = store;
...
```

From the console in the browser, run `window.store.getState()` and make sure you get back the same object as provided in initial state and wired into the reducers.

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