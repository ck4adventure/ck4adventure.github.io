---
layout: post
title: Enterprise Django
category: dev
---

Dinder says a person could use git remotes to have three separate repos going. I find that overkill, three branches off the same repo is more than enough to cover dev/staging/prod. CI and/or Heroku is configurable enough to build those branches.

He also barely covers CI/CD and containers in the first chapter. I seriously hope he gives an example and doesn't revert to procfiles. **fingers crossed**.  

Interestingly, finally an example of how `ALLOWED_HOSTS` should look
```py
ALLOWED_HOSTS = [
'your-domain.com',
'www.your-domain.com',
'dev.your-domain.com',
'staging.your-domain.com',
'becoming-an-entdev.herokuapp.com',
'mighty-sea-09431.herokuapp.com',
'pure-atoll-19670.herokuapp.com',
]
```

And what NOT to do:
```py
ALLOWED_HOSTS = [
'*',
'.your-domain.com',
]
```

### .env files
Python follows the same conventions as node, yay! So now there is a `.env` in my repo which is gitignored and holds my sensitive secrets data and other env dependent variables. For now I have set my secret keys to something fun but not easily hackable, and later in the book I'll learn how to generate properly secure keys.

To add them to heroku from the cli (must be logged in): `heroku config:add SECRET_KEY=<key> --app <app name>`

### Procfiles
SMH. Here we are yet again with a procfile.

So far, this is what we've got, which cd's into the app and then requests the wsgi file  
```py
web: sh -c 'cd ./app/ && exec gunicorn app.wsgi --log-file -'
```

### Static Files
First add `'whitenoise.middleware.WhiteNoiseMiddleware',` to the list of middlewares in the settings file.

And further down, these replace `STATIC_URL`

```py
STATICFILES_STORAGE = 'whitenoise.storage.
CompressedManifestStaticFilesStorage'
STATIC_URL = '/staticfiles/'
STATIC_ROOT = posixpath.join(
*(BASE_DIR.split(os.path.sep) + ['staticfiles'])
)
```

and

```py
MEDIA_URL = '/media/'
MEDIA_ROOT = posixpath.join(
*(BASE_DIR.split(os.path.sep) ['media'])
)
```

!! However, since the printing of this, and me using Django 5, the media root and static root variables were screwing up heroku and so I have left them out, see how it goes.

### DBs

I found this delightful in regards to using `SQLite` as the db, even for a proof of concept.  
> This is not recommended if security is as important to you as it should be.

Dinder then goes on to list how to config not only `SQLite`, but `MySQL`, `MariaDB` (which is just a fork of MySQL and uses the same config), `Oracle` (if you're magically an Oracle admin), `Microsoft SQL Server`, and finally `PostgreSQL`. 

What is needed for  a `heroku` deploy is a bit different than a standard setup. No surprise there.