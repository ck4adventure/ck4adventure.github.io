---
layout: page
title: Rails Responses
permalink: /rails-api/
---

### Views

.html.erb

### Jbuilder

.json.jbuilder



#### Testing with window

```js
// app/javascript/packs/application.js
import { allRanks } from './reducers/selectors.jsx';

...
// inside eventlistener block
  window.store = store;
  window.allRanks = allRanks;
...
```