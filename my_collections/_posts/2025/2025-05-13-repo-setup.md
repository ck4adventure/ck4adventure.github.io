---
layout: post
title: Initial Repo Setups
category: project
---


# Initial Setups

## Nest.js Backend
First I checked my Node version managed by `nvm`, I had been using the current LTS of 22.15.0, but, since the next LTS Node of v24 came out last week, I decided to bump up to that and start using it for all my projects. 

Then I installed the nest cli, and created my backend project with `nest n [project-name] --strict`, choosing npm as my package manager. The Nest boilerplate project starts out with eslint and formatting set up, which is super nice. I chose `--strict` on project creation to enable typescript strict rules. Once installed I ran the server and checked `localhost:3000` with Postman to verify it did indeed send back a "Hello World" text. This was then pushed to github as an initial commit for the repo.

## Vite React Frontend
Creating a new vite react frontend was also a snap. Their docs are nice and easy to follow along, and this was all it took to get a boilerplate react app up `npm create vite@latest bakeshop-web -- --template react-ts`, with support for typescript. Once I verified a page could load at `localhost:5173`, I committed the initial repo. 

Next up was tailwindCSS, which again, super easy to install and config to work with Vite. The command `npm install tailwindcss @tailwindcss/vite` installs everything, and then it is just a matter of plugging it into the vite app config `vite.config.ts`, and adding the line `@import "tailwindcss";` into the index.css file. That was committed, and then it was time for my components via shad/cn.

## shad/cn Component System
I had forgotten that the shad/cn docs provide pretty much this entire setup, but it's helpful to know I'm on the right track. After updating the compiler options in the tsconfig files, I ran into a familiar problem on init: [It looks like you are using React 19. Some packages may fail to install due to peer dependency issues in npm](https://ui.shadcn.com/react-19). My options are to force the install and override any peer dependency conflicts, or skip checks and allow installation of any packages that may have unmet peer dependencies. Or, after visiting that link, I can downgrade to React 18 until all of shadcn is ready. There is a handy chart which shows that the radix react-icons are the only thing left with a PR open, so I feel pretty comfortable choosing to allow the `--legacy-peer-deps` flag to skip the checks, which it turns out was the old behavior in older npm versions, and still in place with yarn, bun, and pnpm. `--use-force` is the more agressive version that will also force other failing checks, so legacy deps is the more standard choice.

Now that I've completed the shadcn init, I add a Card component to check that it displays on the main page and it's good to go.

## Secrets Management Strategy
It's interesting that chatgpt would put this in before the backend framework is in place, but I can see where it's a decision to be made as early as possible. I prefer `.env` files for keeping my secrets safe, first insuring it's on the `.gitignore` and never committed, and using the `dotenv` package to retrieve them in my code. Once it's deployed the prod secrets would be entered into environment variables and made available that way. I looked up how github actions works with managed secrets in their yaml files as well, good to know for later.