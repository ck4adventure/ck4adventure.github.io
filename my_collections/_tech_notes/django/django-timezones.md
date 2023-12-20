---
title: Django and Timezones
topic: django
---
When working with datetime objects in python, it often requires the use of the datetime module. There are tz "aware" datetime objects and "naive" ones that do not know their timezone. Regular datetime objects are naive and don't know their tz. `is_aware()` and `is_naive()` are methods to determine whether or not a datetime object is naive or not. This is important because of `USE_TZ=True` in the app conf (which is best practice). 

The old way, which can have issues during daylight saving time transitions:
```py
import datetime

now = datetime.datetime.now()
```

There are some django.utils built just for this:
```py
from django.utils import timezone

now = timezone.now()
```

From the docs:
> In practice, this is rarely an issue. Django gives you aware datetime objects in the models and forms, and most often, new datetime objects are created from existing ones through timedelta arithmetic. The only datetime that’s often created in application code is the current time, and timezone.now() automatically does the right thing.

This example shows how the two modules can work together:
```py
import datetime

from django.db import models
from django.utils import timezone


class Question(models.Model):
    # ...
    def was_published_recently(self):
        return self.pub_date >= timezone.now() - datetime.timedelta(days=1)

```

