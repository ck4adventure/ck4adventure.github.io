---
layout: page
title: Vite React
topic: react
---
### Basic Setup
(yarn or npm interchangeable)
- Ensure you are using node: `nvm use lts/iron`
- Vite as the HMR dev server `yarn create vite <app-name> --template react-ts`
  - React as the FE framework
  - TS for type checking
  - ESLinters for ensuring format and structure
- `yarn add eslint eslint-plugin-react --save-dev`
- `git init` -> vite already created a nice .gitignore for us
- `yarn add @reduxjs/toolkit` -> redux for js
- `yarn add react-redux` -> redux for react
- `yarn add react-router-dom` -> browserRouter
- `yarn add axios` -> data util that handles the api calls

### Using MUI components system
MUI adds
- `yarn add @mui/joy @emotion/react @emotion/styled` -> new MUI library for components
- `yarn add @fontsource/roboto` -> MUI's preferred font
- `yarn add @mui/icons-material`
JOY adds
- `yarn add @fontsource/inter` -> Joy's preferred font, usage `import '@fontsource/inter';`

CSS regular
- `yarn add sass`

### Routes File
`/src/routes/routes.tsx`
```
import {
  createBrowserRouter,
} from "react-router-dom";

export const router = createBrowserRouter([
  {
    path: "/",
    element: <RootPage />,
    errorElement: <ErrorPage />,
  },
  {...},
])
```
