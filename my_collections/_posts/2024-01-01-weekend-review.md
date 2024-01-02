---
layout: post
title: New Year's Weekend
category: dev
---

I got the itch to see just how hard it would be to get a `dockerized` Django app into production this weekend and it took quite a bit. There aren't a lot of notes from trying out all the different things and reading various tutorials. Most start out with a specific template with all their internal settings figured out. But it's exactly the little details of getting Django production ready that are still missing. I did however learn/remember quite a bit of docker and could successfully locally run my django app in a container. It was just getting it deployed with an apache server and in production mode that became more challenging.

Bejeweled was a really fun game from the early 2000s and is also something that I'd like to someday code for myself. I found [a good example](https://inventwithpython.com/blog/2011/06/24/new-game-source-code-gemgem-a-bejeweled-clone/) by the same author of Automate the Boring Stuff. After spending a day on it Sunday to give myself a break from docker, I realized learning game logic in no way helps me forward on my career hunt so that will wait a while until I get other projects out.

Sunday evening and Monday was back to Django. I feel I just don't know enough quite yet, so it's back to the Django docs with my newly gained knowledge of Python basics. I also found another source of wisdom that I think will help [Becoming an Enterprise Django Engineer](https://www.scribd.com/document/619193574/M-Dinder-Becoming-an-Enterprise-Django-Developer-Discover-Best-Practices-Tooling-And-Solutions-for-Writing-and-Organizing-Django-Applications-in) on a free trial from `Scribd`

### Why Django?
It holds all the modern features and paradigms necessary to build an enterprise application. It can be used for regular pages with content supplied by templates, but also function as an API backend for React FE or native Android and iOS apps.

### Types of APIs
- public
- partner (outside access upon permission)
- private (internal)
(Not that this matters in the initial phases of development at all, just deployment)


### Designing and Planning
These are my strong skills, and yet I still enjoy reading how other people approach it. I like to follow best practices, which include detailed acceptance criteria and an actual understanding of the use case.

>  If your developers are not provided with enough documentation,
blueprints, and other materials, then they will be left to make assumptions on their own,
assumptions that later on are found in the testing and Quality Assurance (QA) phases
of development as bugs in your application. 

I wish more CEO's followed that advice.

User Research and creating `User Stories` is still key.

> For smaller projects, you are free to design something yourself, but that often takes up time and developers often experience a type of writer's block when tasked with actually designing something versus building something.

**Wow**. Now I don't feel quite so bad.

#### Diagramming
I do like creating infographics, it's a skill I've had some practice at and is very satisfying when others can look at it and `just get it`.

- Activity diagram
- Class diagram
- Communication diagram
- Component diagram
- Composite diagram
- Deployment diagram
- Entity relationship diagram
- Flowchart
- Interaction diagram
- Object diagram
- Package diagram
- Profile diagram
- Sequence diagram
- State diagram
- Timing diagram
- Use case diagram

`Class diagrams`: class diagrams depict the objects that would be tables in a database, the interactions that could take place, and any other main elements of your system.

```
Class: Ingredients
- name
- measure
- belongs_to recipes through Recipe Ingredients
Functions:
- find_recipes_with_ingredient
```

`Deployment diagrams`: This is how developers will collaborate and code will be updated between different environments. It is mostly a high level overview 
- a node as a physical entity that executes a part of system or process
- a device is a node that is a computational resource
- an artifact is a digital asset, whether a script, image or executable

`Entity relationship diagrams`: sometimes called an entity relationship model after modeling relationships in a database. These are used by your backend to help create the structure of the database and what fields should be included. They can also be generated from an existing database.

`Flowcharts`: Flowcharts represent the flow of data within the system. They provide a step-by-step approach to solving a particular problem or task.

`State diagrams`: A state diagram shows the behavior of objects within a system. The diagram shows possible conditions or states that something can be in at any given time, such as depicting whether a user is either logged in or logged out; an order is either received, processing, or out for delivery, or an order is fulfilled or returned.

`Use case diagrams`: A use case diagram represents the behavior of a user and the system. These are fairly similar to a flowchart but often focus on the bigger picture.