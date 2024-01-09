---
layout: post
title: DBs and Apps in Prod
category: dev
---
Woke up this morning feeling resolute. My month of taking it easy is over, time to really spend some hours coding and learning. Every time I have to log in to one of my fitness studios I am reminded how much of a gap is left in this market as well.

### Postgres, Django, and Heroku
The settings for configuring Django to postgres are super easy, but apparently not when using Heroku. But here we are still.

One cool thing I learned is that the Heroku CLI is nicely built out. And I did figure out how to clean out old dbs on my local postgres via Postico. 

There is a lot of postgres connection that is just skipped over, so I'm not exactly certain what I've done is going to work. I don't know Django well enough to know for sure, but what Dinder is having me do is not how the docs seem to approach it. 



I do like the reference list of data types
|  |  |  |   |
| --- | --- | --- | --- |
| AutoField | BigAutoField | BigIntegerField | BinaryField |  
| BooleanField | CharField | DateField | DateTimeField |  
| DecimalField | DurationField | EmailField | FileField |  
| FilePathField | FloatField | ImageField | IntegerField|  
| GenericIPAddressField | JSONField | NullBooleanField |  PositiveBigIntegerField | 
|  PositiveIntegerField | PositiveSmallIntegerField | SlugField | SmallAutoField |  
| TextField | TimeField | URLField | UUIDField |  


...




Ok, enough of that weirdness, back to the Django docs.
