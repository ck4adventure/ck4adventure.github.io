---
layout: post
title: the 12 factor app
category: cs
---

While reading the gorilla/mux readme/docs on github this morning I was thinking about testing practices and best practices in general when I remembered about the 12 Factor App. I believe it is fairly "old" at this point, most of these practices have become industry standord, and when I think about the context of what the development environment was like that this was considered novel and necessary, was probably mid to late-2000s, around the fail-whale era. 

### The 12 Factors
(for a professional and stable web service)

Brief list for easy memorization:
1. Maintain a code revision history and all deploys from the same code repo.
1. Use a package/module manager for dependencies. Ruby gemfile, npm package.json, go mod
1. Do not hardcode config variables, use env files and inject them in
1. Attached resources should be swappable without changing code, just config
1. Versioned releases, build/test => release => run server
1. The app should be stateless and not rely on local memory to store persistent data
1. App works by exporting HTTP by binding to a port, and listening to requests coming in on that port. Should not rely on something else to serve it (go http vs apache)
1. Rely on external process manager to manage the app's process (no pid files), scaling horizontally should be easy
1. Disposability: fast startup, graceful shutdown. Use code wrappers to handle start/stop of server.
1. Dev/prod parity. Keep them as close together as possible in terms of code, incl db and attached resources.
1. The app itself does not write logfiles, all stdout is to be collected and handled by the execution environment (env) in which the app is running.
1. Admin and maint tasks should be shipped alongside app code as executable actions, just ssh in and run them.
