---
layout: page
title: React Basics
permalink: /_pages/react/react-basics/
---

# React Hooks

## State Hooks

Reacts way of handling local state without using a class

```js
const [name, setName] = useState(inital_value);
...

setName(new_value);
```

## (Side) Effect Hooks

These take the place of lifecycle component methods such as `componentDidMount`. Make sure to include the empty array of watched variables when performing fetches so as not to loop.

```js
useEffect(() => {}, []);
```

# Redux Hooks

## useSelector

This replaces the `mapStateToProps`, it takes a function that takes in state (the selector you've already written can be used) and returns the slice of it you need.

```js
const arcaneWeapons = useSelector((state) => state.weapons.arcane);
// OR
const arcaneWeapons = useSelector((state) => toArray(state.weapons.arcane));
```

## useDispatch

```jsx
import { useDispatch } from 'react-redux'
...
return (
  const dispatch = useDispatch()
  ...
  <button onClick={() => dispatch({ type: 'increment-counter' })}>
)
```

## Older React

#### Wrap Provider and Hash Router

#### Class Component Container

import connect
import actions and selectors
mapStateToProps
mapDispatchToProps
export line

#### Class Components

constructor
lifecycle methods

- componentDidMount
- componentDidUpdate
- compononentWillUnmount
  render
  binding any passed action handlers

# Functional Components

depend on props being passed to them
more reusable, less overhead



## Links and Routes
