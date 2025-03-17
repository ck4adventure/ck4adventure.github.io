---
layout: post
title: First Django Session
category: django
---

### Creating the Project
Since this is python, I prefer to maintain a `python_projects` folder for all of my personal projects and within that I use `venv` to maintain a python virtual env. So happy to finally have `source ./venv/bin/activate` in my fingertips. It's always good to check and make sure where things are with `python --version`, mine is currently set to 3.12. While reading the docs I read that Django just went through a major update, so I updated to v 5.0 for the fun of it with `python -m pip install -U Django` and confirmed with `python -m django --version`. Now I'm ready for that pollsapp, lol.

But really, the tutorial is a great way to start. 

First step is to use django to create a skeleton app framework with `django-admin startproject <name>`. Name in this case should be the name of whatever your main appname is that the server is running, as it will be used for imports. For now I'm calling mine "practice".

A quick `ls` verifies for me that indeed a new folder has been created and I `cd` in. 

At the top level there is only a file and another folder named `practice`. The file is the `manage.py`, which first ensures the settings module is pointed at the project before then passing the command along to django for execution. It follows all the same commands as listed for `django-admin`. As far as I understand it, this is analagous to calling `rails` in a rails project. Usage `manage.py <cmds>`.

Within the folder, also called `practice`, is now my app. 
- `__init__.py` is a convention which informs python that this folder should be treated as a package, it can be left empty. 
- `settings.py` contains project settings, and I know I'll be coming back around to those later once I'm ready to switch to pg, amongst other things.
- `urls.py` holds the routes structure for the entire app. I am curious what best practice will be for keeping them organized.
- `wsgi.py` and `asgi.py` are the web server and async server gateway interfaces, which are the two specifications for running web servers in python.

Back to making things happen, from the outer `practice` directory, ensure the server works with 
`python manage.py runserver [<port>]`. NB this development server is not a production ready server. Also, although it can hot reload on file changes, it must be restarted on file additions.

### Creating the App
Now we can start creating an app with `python manage.py startapp polls`. This creates a `polls` dir at the top level and within that is a new set of files. Enough is in place that a basic route can be added that returns a response.

First, the "view" needs to know what to send back.

`views.py` within the `polls` dir.
```py
from django.http import HttpResponse

def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
```

Next, create a urls file `touch ./polls/urls.py`, and add the following.
```py
from django.urls import path
from . import views

urlpatterns = [
    path("", views.index, name="index"),
]
```

Finally, hook the apps urls into the main server configuration in `urls.py` at the top level.
```py
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path("polls/", include("polls.urls")),
    path('admin/', admin.site.urls),
]
```

`include()` as used above is explained by the docs:

> The include() function allows referencing other URLconfs. Whenever Django encounters include(), it chops off whatever part of the URL matched up to that point and sends the remaining string to the included URLconf for further processing.

`path()` as used above can take the following arguments:
- `route`: this is the string which is the URL pattern to be matched. Python reads the list from top to bottom and goes with the first match it finds. 
- `view`: this tells python which view function to run. When it is called, python will first pass in an object as the request, and then any additional captured values.
- `kwargs`: arbitrary keyword arguments that can be passed in
- `name`: a name allows the url to be referenced from anywhere in the project

### Hooking in a db
At this point if it were a postgres db, there would be a need to stop and set that up, through either a docker container running a pg instance or running pg locally on my machine. However, python has sqlite3 which runs off of local files, which is enough for getting started with django concepts.

The db settings are in `<appname>/settings.py`. Since I didn't specify anything other than the default when creating the practice project, sqlite3 has already been set as the db `ENGINE`, and it's file created for me in the root dir, the path of which is listed under the `NAME`. I verify that before scrolling down even further and setting the `TIME_ZONE` to 'America/Los_Angeles'. I will go back and dig in later to confirm that this just informs the physical location of the server, since `USE_TZ = True` is also set by default, which tells the app to always store datetimes in UTC.

Finally, it's time to run the migration and get rid of the pesky warnings `python manage.py migrate`

### First DB model
Django believes the data model should be defined in one place and everything derives it's data from that. This extends to migrations, where unlike rails:
> migrations are entirely derived from your models file, and are essentially a history that Django can roll through to update your database schema to match your current models.

Example models in practice/polls/model.py 
```py
from django.db import models


class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField("date published")


class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```

Question and Choice both subclass the Model Class. Each class variable represents a field in the database. It's name will be used as the column name. The field must be assigned one of the many Field types available, some types take additional arguments, some do not.

Once the models are how we like them, ensure the polls app is imported through the settings file, which ensures it gets picked up by the db. The module name is the folder name.

settings.py
```py
INSTALLED_APPS = [
    "polls.apps.PollsConfig",
    'django.contrib.admin',
    ...
]
```

Finally, in order to migrate the new model into the db we run:
`python manage.py makemigrations polls`

```bash
Migrations for 'polls':
  polls/migrations/0001_initial.py
    - Create model Question
    - Create model Choice
```
