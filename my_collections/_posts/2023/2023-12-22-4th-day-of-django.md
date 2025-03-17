---
layout: post
title: 4th Day of Django
category: django
---

### Review
Yesterday I worked with templates, getting to know template tags and code interpolation within html again. Django has quite a few convenience wrappers, such as being able to reference a path by name along with whatever url params it needs within the template tags. The request.METHOD object can be indexed into for those params within the view method. And view methods have a handy `reverse` function which can take a path name and arguments and lookup the url.

There is also an interesting feature called `generic views` in which there are pre-built view methods to try/except looking up an item's data and pass it to the template. All that is needed is a Model name and the template the final data should go to. I am curious how much this is used in production apps and whether or not it saves developer effort.

### Testing
I really, really admire the introduction to testing written up by the Django docs team. From day one at my coding school testing was emphasized as well, and what I learned there has paid off in real life. Real projects are messy and devs often have their own unconscious ways of doing things. It's actually the small little details like `error` vs `errors` in a response that can take up a lot of debug time to track down and fix. And writing tests forces the dev to really understand the goal of what they're creating. I've had many a debugging session where I've come across tests that did not fail properly, and every time it was because the dev writing them had not understood the task they were given (and sadly didn't ask for help). 

Test driven development (TDD) is an ideal that should be followed whenever possible. Truly, no code should ever be written until there is a failing test for it, the reason being is that you always want to see a failing test before getting to pass. Otherwise, how would you know you wrote a proper test?

#### The `shell` as a testing tool
While developing, it can be super helpful to interact with the db models to inspect them, check edge cases and ensure that the data does what is expected. The shell is a great way to import models from the project and django provides utilities to interact with the server endpoints.

First, open the shell with `python manage.py shell`.

To work with data, remember to import any models needed:
```py
>>> import datetime
>>> from django.utils import timezone
>>> from polls.models import Question
```

And then we can test out our methods:
```py
>>> # create a Question instance with pub_date 30 days in the future
>>> future_question = Question(pub_date=timezone.now() + datetime.timedelta(days=30))
>>> # was it published recently?
>>> future_question.was_published_recently()
True
# oops!
```

#### Test files
Creating tests is as easy as translating that shell interaction into a repeatable set of code. Update the tests.py file in the polls dir as follows to enable a unit test:

```py
import datetime

from django.test import TestCase
from django.utils import timezone

from .models import Question


class QuestionModelTests(TestCase):
    def test_was_published_recently_with_future_question(self):
        """
        was_published_recently() returns False for questions whose pub_date
        is in the future.
        """
        time = timezone.now() + datetime.timedelta(days=30)
        future_question = Question(pub_date=time)
        self.assertIs(future_question.was_published_recently(), False)
```

Now we have a test that we can run, which we can do with the command:  
`python manage.py test polls`  

A lot of things happen: 

- `manage.py test polls` looked for tests in the polls application
- we put the code in an easy for devs to find `tests.py` file, and within that `test` found a subclass of the django.`test.TestCase` class
- it created a special database for the purpose of testing
- it looked for test methods - ones whose names begin with `test_`
- in `test_was_published_recently_with_future_question` it created a Question instance whose pub_date field is 30 days in the future
- and using the `assertIs()` method, it discovered that its `was_published_recently()` returns True, though we wanted it to return False (same as we saw in the shell) 

Fixing the code as follows will make it so the tests can pass:  

tests.py
```py
def was_published_recently(self):
    now = timezone.now()
    return now - datetime.timedelta(days=1) <= self.pub_date <= now
```

There are more test cases that should be written in as well, for example another test to verify that it returns false when indeed the pub date is older than one day, and a test to verify it returns true when the pub date is less than one day. Every test written builds a set of "safety rails" for the application that helps to keep errors (at least in terms of i/o and business logic) to a minimum.


#### Client as a testing tool
Django comes with a Client tool to be able to interact with the app as if making HTTP requests externally like a user client would (ie a web browser). This sets up a template renderer, but does not set up a test database, it needs to be run on an application running with a database. For the purpose of the tutorial, this is incredibly easy since the db is sqlite3.

When in the `shell`, it can be imported:  
```py
>>> from django.test import Client
>>> # create an instance of the client for our use
>>> client = Client()
```

And then we can do things with it:
```py
>>> # get a response from '/'
>>> response = client.get("/")
Not Found: /
>>> # we should expect a 404 from that address; if you instead see an
>>> # "Invalid HTTP_HOST header" error and a 400 response, you probably
>>> # omitted the setup_test_environment() call described earlier.
>>> response.status_code
404
>>> # on the other hand we should expect to find something at '/polls/'
>>> # we'll use 'reverse()' rather than a hardcoded URL
>>> from django.urls import reverse
>>> response = client.get(reverse("polls:index"))
>>> response.status_code
200
>>> response.content
b'\n    <ul>\n    \n        <li><a href="/polls/1/">What&#x27;s up?</a></li>\n    \n    </ul>\n\n'
>>> response.context["latest_question_list"]
<QuerySet [<Question: What's up?>]>
```

But it also exists within the test tooling, and can be referenced within the test file. Note at the top a helper method so that we can create new questions easily, and the naming conventions to help convey each possible situation and outcome. In an ideal world, the bulk of these should be coming in as acceptance criteria for the feature being built, and there will be a lot of them.   

`tests.py`
```py
# make sure to import the reverse method to be able to look up endpoints
from django.urls import reverse

def create_question(question_text, days):
    """
    Create a question with the given `question_text` and published the
    given number of `days` offset to now (negative for questions published
    in the past, positive for questions that have yet to be published).
    """
    time = timezone.now() + datetime.timedelta(days=days)
    return Question.objects.create(question_text=question_text, pub_date=time)


class QuestionIndexViewTests(TestCase):
    def test_no_questions(self):
        """
        If no questions exist, an appropriate message is displayed.
        """
        response = self.client.get(reverse("polls:index"))
        self.assertEqual(response.status_code, 200)
        self.assertContains(response, "No polls are available.")
        self.assertQuerySetEqual(response.context["latest_question_list"], [])

    def test_past_question(self):
        """
        Questions with a pub_date in the past are displayed on the
        index page.
        """
        question = create_question(question_text="Past question.", days=-30)
        response = self.client.get(reverse("polls:index"))
        self.assertQuerySetEqual(
            response.context["latest_question_list"],
            [question],
        )

    def test_future_question(self):
        """
        Questions with a pub_date in the future aren't displayed on
        the index page.
        """
        create_question(question_text="Future question.", days=30)
        response = self.client.get(reverse("polls:index"))
        self.assertContains(response, "No polls are available.")
        self.assertQuerySetEqual(response.context["latest_question_list"], [])

    def test_future_question_and_past_question(self):
        """
        Even if both past and future questions exist, only past questions
        are displayed.
        """
        question = create_question(question_text="Past question.", days=-30)
        create_question(question_text="Future question.", days=30)
        response = self.client.get(reverse("polls:index"))
        self.assertQuerySetEqual(
            response.context["latest_question_list"],
            [question],
        )

    def test_two_past_questions(self):
        """
        The questions index page may display multiple questions.
        """
        question1 = create_question(question_text="Past question 1.", days=-30)
        question2 = create_question(question_text="Past question 2.", days=-5)
        response = self.client.get(reverse("polls:index"))
        self.assertQuerySetEqual(
            response.context["latest_question_list"],
            [question2, question1],
        )
```

What starts to feel like a bloated test suite is actually to be expected. Having tons of tests is ok, they can only help. Some nice guidelines from the docs:
- a separate TestClass for each model or view
- a separate test method for each set of conditions you want to test
- test method names that describe their function

#### Additional testing notes
- Selenium for testing the rendered output as it would appear in a browser, which is useful for checking any javascript functionality from within the pages
- it's possible now to use CI (continuous integration) to run the test suite on each code commit
- `coverage.py` to keep track of how much of the code is "covered" by tests
- more information on testing [from the django docs](https://docs.djangoproject.com/en/5.0/topics/testing/)