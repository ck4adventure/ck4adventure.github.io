---
layout: post
title: Small Framework Digression
category: cs
---

# Small Digression into Backend Frameworks
Last week as I started down the path of setting up repos, the first thing I did was head over to the [Nest.js docs](https://docs.nestjs.com/), and start reading up on what it is as a framework and how to get started. Nest uses the dependency injection design pattern, which I must admit I have not used in any of my previous roles. So I took a little extra time across a few days to read up on it, understand the use of decorators for dependency injection and just getting to know decorators in general. I had chatgpt make me a [cheat sheet](/sheets/modern-javascript-since-es6.html) to be able to review what was added when. Which, it turns out, comes from Typescript. 

Which reminds me that although I have a couple of books on Typescript that I've attempted to read through, neither really offered information structured in a way that I was easily able to process. So today I also asked chatgpt for a quick rundown on how typescript differs from js, and got [this list](/sheets/typescript-vs-javascript.html). It was a great reminder of how classes look in TS since so far I've only made simple react components and not done any class based work.

So finally today I am ready to start working with NestJS and learning to build using their decorators and patterns. Here are a few commands to remember for later:

```ts
npm i -g @nestjs/cli
```

```ts
nest new project-name
// alias n
// optional --strict flag for a stricter feature set
```

```ts
npm run start
// uses localhost:3000
// npm run start:dev will start with watch mode on
```

```ts
nest generate [boilerplate item]
// alias g
// such as nest generate controller Cats
```

Boilerplate CRUD controllers for a resource:
```ts
nest g resource [name]
```
