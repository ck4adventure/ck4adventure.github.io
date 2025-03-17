---
layout: post
title: Definitive Guide to Javascript
category: js
---

Started reading 'Javascript, The Definitive Guide' by David Flanigan straight through from the beginning. What's great is that I can read it so much more easily now, the first seven chapters at least were straightforward and mostly just affirming that I know what I should know. 

My knowledge isn't perfect, however, and it was also great to fill in a couple gaps I didn't know were there. Such as:

#### Nullish Coalescing Operator = ??
This operator `??` is used when a typical boolean might fail, the easiest example of this would be taking measurements for a physical object and having an inputted measurement of 0 read false. So instead the null coalescing operator returns true as long as the value has been defined.

#### Loops can have labels
Labeling a loop in the allows it to be accessed across any nested scope within itself, basically allowing nested loops to short-circuit their parent loops as well.

#### Reminder of Functional vs Class-Based Programming
It had just come up in an interview call, how much did I know about functional programming. Turns out much more than I realized - I had implemented a very efficient sharing algorithm using functional programming style back at Synthesis. By iterating on the results I was able to transform them and order them into groups according to how many query 'buckets' they could fit into. It was a great achievement after many developers had put their heads to it and not had a solution.