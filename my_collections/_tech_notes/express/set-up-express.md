---
layout: page
title: Set Up Express
topic: express
---

### Initial Setup
`mkdir <name>`
`cd <name>`
`nvm use lts/iron`
`yarn init`
`touch .gitignore`
`echo "/node_modules" > .gitignore`
`touch README.md`
`touch .nvmrc`
`echo lts/iron > .nvmrc`
`yarn add express`
`touch index.js app.js`

### Create App
Update app.js:
```js
import express from "express"
export const app = express()

app.get('/', (req, res) => {
  res.send('Hello World!')
})
```

Update index.js:
```js
import { app } from './app.js'
const port = 3000

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})

```

Run `node index.js` from the root directory to start server.
Ping `http://localhost:3000/` from cURL or a fun GUI like Postman.

