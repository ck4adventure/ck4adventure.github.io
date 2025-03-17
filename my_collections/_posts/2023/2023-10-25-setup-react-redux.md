---
layout: page
title: React-Redux
topic: react
---

An `action` is an object that describes a change to the global state. An action must be `dispatched` to the store where a `reducer` contains logic to receive the action and any data supplied with it and update the state accordingly. Although it seems like actions are defined within reducers, they can actually exist across multiple reducers to affect multiple `slices` of the state with a single action.

When defining a `slice` of state it is given a name, an `initial state` which is super useful to have data to display before the app can even get responses back from a server, and a list of reducers to define which actions that slice of state will respond to, and what it will do for each of those actions and data.

Immutability is the concept of a static value that cannot be changed. *In order to update values immutably, your code must make copies of existing objects/arrays, and then modify the copies.* This is accomplished by array / object spread operators, as well as array methods that return new copies that can be updated.

## 2024 Redux Pattern
- so handy that I know the old concepts to understand the new way
- create a features folder that handles business logic for each feature
- for example, if the feature is a number counter button, folder called 'counter' and file called `counterSlice`
- give a name, inital state, reducers
- generates the actions and their payloads (action type and payload (which is typed, ugh)), using the name and reducer names, so choose wisely
- redux now uses immer under the hood (which also explains devs jumping to Zustand)
- immer handles the immutability of the state for us
- typescript requires additional file to wrap standard hooks aliased with their types, which is a nice meta pattern
- still have to setup a `store.ts` file that combines all the slices
- thunks are the concept of wrapping an api call so that the application can do other things while it waits for data to come back
- ie, a loading spinner
- so an action would be dispatched, and it would have a pending, resolved, and rejected set of code logic to follow
- this is available via extraReducers and builder functions in redux toolkit
- ReduxToolKit TRK is about to have a feature that will write all this for you

## 2018 Redux Pattern

### Wiring in the Framework

#### Entry File
Wherever React and React DOM combine to render the root element into the html tag given is considered the app entrypoint. Here a store `provider` is put in as an element around the entire react app, allowing it to be accessible to all components. Here is where initial state could also be passed in.

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
Compose overwrite is to allow redux dev tools, super nice.

```js
import { applyMiddleware, createStore, compose } from 'redux'
import thunk from 'redux-thunk'
import logger from 'redux-logger'
import rootReducer from '../reducers/root_reducer'

const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;

const configureStore = (preloadedState = {}) => {
  return createStore(rootReducer, preloadedState, composeEnhancers(applyMiddleware(thunk, logger)));
}

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