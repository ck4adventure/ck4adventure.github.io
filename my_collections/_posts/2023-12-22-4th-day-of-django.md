---
layout: post
title: 4th Day of Django
category: dev
---

### Review
Yesterday I worked with templates, getting to know template tags and code interpolation within html again. Django has quite a few convenience wrappers, such as being able to reference a path by name along with whatever url params it needs within the template tags. The request.METHOD object can be indexed into for those params within the view method. And view methods have a handy `reverse` function which can take a path name and arguments and lookup the url.

There is also an interesting feature called `generic views` in which there are pre-built view methods to try/except looking up an item's data and pass it to the template. All that is needed is a Model name and the template the final data should go to. I am curious how much this is used in production apps and whether or not it saves developer effort.

### Testing
I really, really admire the introduction to testing written up by the Django docs team. From day one at my coding school testing was emphasized as well, and what I learned there has paid off in real life. Real projects are messy and devs often have their own unconscious ways of doing things. It's actually the small little details like `error` vs `errors` in a response that can take up a lot of debug time to track down and fix. And writing tests forces the dev to really understand the goal of what they're creating. I've had many a debugging session where I've come across tests that did not fail properly, and every time it was because the dev writing them had not understood the task they were given (and sadly didn't ask for help).


