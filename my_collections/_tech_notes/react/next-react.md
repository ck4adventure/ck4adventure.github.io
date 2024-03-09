---
topic: react
title: Next.js as a React Framework
date: 2024-02-01
---

Front end web technology has indeed come full circle. Server side rendering of React seems like it might solve a few problems, so I am learning it to find out more

### Setup
`npx create-next-app@latest`

Defaults to Ts, a src folder, tailwind css, and some decent initial settings. So far, so good.

### Structure
TODO: go back and write up key points

### Routing Basics
Next uses the file folder system as the basis for the routes. `app` is the top level folder, and from there subfolders can be nested as needed to create the route paths. Each folder should contain certain items, such as the page.ts/js file which contains the UI for that page. 

There is a root folder, many segments, and finally segment leaves as the last subfolder for each route path.


### Server Side Rendering
This is how Next works by default, it utilizes server side components

Some quick benefits
- faster data fetching, closer to the source
- higher security since things like tokens and api keys are kept on the server
- cached results can be stored on the server
- small/no bundle size so that the client doesn't bear the brunt of the js load
- initial load and `first contentful paint (fcp)` are much faster since html is already created and user doesn't have to wait for js to load, execute and paint
- seo improvements cuz bots can read the generated html when they visit
- streaming - the rendering work can be split into chunks and sent as they become ready