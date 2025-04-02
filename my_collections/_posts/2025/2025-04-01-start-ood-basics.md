---
layout: post
title: Object Oriented Programming
category: cs
---

Object Oriented Design is a programming style

So then of course I realize I can't name the other styles / paradigms off of the top of my head.

### Imperative Programming
`Imperative programming` focuses on how to perform a task step by step. First do this, then that, and the next, etc. Each statement will change the programs state in some way.
A sub-paradigm is `procedural programming`, where code is organized into procedures or functions.

Running a loop that reads a value from the array and updates a total sum is an example of imperative programming.

### OOP
In object oriented programming, objects contain both `state` and `methods`.

A racecar class might inherit from a vehicle class the start and drive methods, but have its own method called makePitStop. 

### Functional Programming
Uses pure functions that don't change state, focuses on what to do not how to do it.
In js, `map` and `reduce` are examples.

### Declarative Programming
Describes what the program should accomplish, not how.
This includes:
- Logic Programming: Uses rules and facts (e.g., Prolog).
- SQL (Relational Programming): Query-based approach for databases, the db engine figures out the rest.
- Markup and Styling Languages: HTML, CSS.

### Event driven programming
Events are listened for, and trigger the associated function to occur once they happen.
An example is a mouse click on a button triggers a modal to display.

### Other types
#### Reactive JS RxJS for handling streams of data that change over time
#### Prolog engine can deduce facts from structures of data

## Basic Concepts Used in OOP
Attributes - information unique to an object, thats its `state`
Methods - perform actions, usually related to the attributes
Classes - blueprints for creating instances of an object
Objects - the actual instance that exists and can be used in the code

## Basic Principles of Object Oriented Programming
- abstraction, using screens and other user interfaces abstract away what the program does from how it does it, methods are the abstractions
- encapsulation, keeping necessary information hidden away from the rest of the program so it can't be changed except by exposed getters and setters
- inheritance, copy with attrs and methods from a parent class as a starting point, helps with reusability  
	- inheritance can be single or multi level  
	- items can inherit from multiple parent classes  
	- a single parent class can have many children classes inherit from it  

The four advantages of inheritance:
- reusability
- code modification
- extensibility
- data hiding / encapsulation

Polymorphism is the concept of many forms, and can be achieved through `method overriding`. 

`Method overriding` is when a child class defines a method it has already inherited from a parent class. The child class's method overrides the parents. The term for doing this is dynamic polymorphism.

By contrast, there is also `method overloading`, where multiple methods are defined with the same name, but differ in the number or type of arguments. This is static polymorphism.

Some languages, but not js, support `operator overloading`, in which the behavior of operators such as '+' are overloaded to handle custom data types

## Object Oriented Analysis and Design
To Analyze, first observe the system and analyze it to determine the objects and relationships between them. Define the roles of each of the objects in the system.

To Design, use the analysis to create the class models and all their details. Often, UML or another set of diagrams is used to show the models and their connections.

