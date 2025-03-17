---
layout: post
title: Forms in Django
category: django
---

### Weekend Review
I finally have a decent Admin page working to create recipes. It's definitely still more of an MVP, but it works, which is the key. I have both a custom joins table for one many-to-many data relation with additional fields, and am relying on built in table functionality for the others until they need more. Also of interest is the `orderable` package I am using from the Python Package Index aka [pypi](pypi.org).

### Templates and Forms
It would seem the standard Django Template Library (`DTL`) is in use by most developers at >80%, followed by `Jinja2`. So after spending some time looking at those two and reading their docs, as well as `Crispy` forms docs, I decided to stick with the standard DTL. 