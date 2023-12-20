---
layout: page
title: Django Basics
---

### Project Setup
- Ensure virtual env and `souce ./venv/bin/activate`
- Ensure it's the python version wanted `python --version`
- Ensure it's the django version wanted `python -m django --version`
- Create new project with `django-admin startproject <name>`
- Ensure project runs with `python manage.py runserver` and visit the url in the output.

### App Setup
From the root project folder `python manage.py startapp <name>`

- Configure view (what in rails is a controller)
- Configure URL (what in rails is a route)
- Ensure url imported into top level

### DB Setup

If using the default sqlite3: `python manage.py migrate` to run the initial migration for system apps as well as any created by me up to this point.