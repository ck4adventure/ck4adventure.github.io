---
layout: post
title: Testing with Jest
category: dev
---

Spent some time this weekend getting tests set up for my latest feature, currently called 'chef' for lack of a better name. Not only do I want to keep up to speed on all the best practices for testing, I want to keep up to speed on different libraries. My picks are Mocha, Jest, and Cypress.

I have Mocha+Chai for my backend schema, I am running that against a local pg test db. Eventually I'll refresh on how to get this all dockerized so that I can run tests within a CI/CD pipeline. But for now I am happy with a more manual setup. Having tests I can run to ensure my db has been initialized/migrated to the proper schema feels so nice. And writing out schema's is a great way to practice some sql. 

For the frontend testing, I am working with both Jest and Cypress to get to know them better. Cypress is my e2e solution, which currently runs against the dev server. This is where I define the basic structure of each page, it is a great way to require me to think about what I want to put on the page as I create the feature. There is a balance, especially while building out an idea without a pre-written spec, of enough tests to define structure, but nothing too detailed so that changes are easier. 

And Jest is for my integration tests, this is the level of testing I am least-practiced in. Having chat-gpt as a part of my daily workflow is great to help me with best practices and explaining them to me. My first set of tests is now built around my server actions, and Jest's test coverage indicator was a real eye opener, plus it actually shows me what I need to look at for achieving 100% code coverage, so I am excited to keep working towards that.