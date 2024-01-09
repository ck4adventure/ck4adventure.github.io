---
layout: post
title: So much to learn!
category: dev
---

I realized I was getting caught in the config weeds of Dinder's Enterprise Django, so I am back to working on my recipe app, still referencing his book for tips, but mainly using the Django docs. 

Working with Models is my topic for today. I have started plugging in my recipe models such as Ingredient, Recipe, RecipeIngredient, and RecipeStep. I have some basic notes on my data schemas, but this makes me realize how important it is to get these things documented, not only to keep myself on target, but to be able to reference later for planning updates and changes. I have a confluence project in the works for my scheduler app, but now I am feeling the pressure to document my recipe app better as well. All I really want to do is code, but I understand the reason for the discipline of documentation. 

And can I just take a minute to rant at all the super lame internet articles and blog posts promising to teach me to do something in code which are just pure bullshit. Most are either recopied from the docs or barely thought out or so simple that there is no value added other than stroking their own ego for having published (I'd be so embarrassed honestly). I really, really hope the rest of the internet sees these junior fakes for what they really are. If I were to take these blog posts and actually try and publish them out for others to use I would do it with _style_ **and** _substance_.

And even trying to write the above line in markdown I just learned that it doesn't support underlining words in text, as underline is reserved for displaying links. Smart.

### Models
Working with models in Django is how I expect things should be. Having learned Rails in school, Django feels comfortable and familiar, working as I would expect as an ORM. (My last role had a ORM-less golang API that was a mess!) Already I am learning to create my own through tables and getting to know all the FieldTypes and their options. Django has some basic built in validators that I can call on as well, saving me some time. 