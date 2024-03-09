It's been a while since I needed to talk BigO. I did get to write an interesting sharing algo which  I need to now review

Created a set of buckets by iterating over each of the queryable properties
gender: m/f
ethnicity: [arab...]
age_group: [0-24,25-34,...]

looked something like
[male][arab][35-44]
[female][black][55-]

very incomplete data set, no arab females of any age
mostly white males of 25-34, some asian and black
lacking in older age groups

query filter was percentage groups that could each specify which of the params to filter on

50% females, any eth, 55-
40% males, black eth, 25-34 and 35-44
10% males, any eth, any age

I used random selection to then 