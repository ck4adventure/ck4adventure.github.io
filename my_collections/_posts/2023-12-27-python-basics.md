---
layout: post
title: Python Basics
category: dev
---

I just came across what I think is a great book on Python called [Automate The Boring Stuff](https://automatetheboringstuff.com/2e/chapter1/) and so I thought I'd write up some notes as I read it, not because I don't understand basic programming, but because I don't always talk about programming with others, so a refresher in the *nomenclature* is important to me, as well as understanding some of the nuances of Python.

The first thing (which I think I had learned once and forgotten) was that Python is not named for the snake, but for the comedy troupe. 

### Basic Concepts
`REPL` stands for Read-Execute-Print-Loop, and is a type of `IDE` Integrated Development Environment. The Python `IDLE` is for Integrated Development and Learning Environment. There is an online environment called [`Mu`](https://codewith.mu/)

`expressions` are statements that contain `values` (like 2) and `operators` like (+) that `evaluate` into a single value (even if that value is sometimes itself a function).

Three operators I don't use often but should remember:
- `**`: exponential operator; 2**3 = 8
- `%`: modulo/remainder of quotient; 22%8 = 6
- `//`: integer division/floored quotient: 22//8 = 2

And their order of operations:
> ** operator is evaluated first; the *, /, //, and % operators are evaluated next, from left to right; and the + and - operators are evaluated last, also from left to right

A `syntax error` is when Python cannot read the code as written.

The most common `data types` in Python are `string` or `str` (pronounced 'stir'), `integer`, and floating-point numbers (`floats`). Strings can use the `+` symbol as a shorthand for concatenation, but unlike some languages, Python will not try to do a type conversion if one of the values is not a string.

```py
>>> 'Alice' + 42
Traceback (most recent call last):
  File "<pyshell#0>", line 1, in <module>
    'Alice' + 42
TypeError: can only concatenate str (not "int") to str
```

It also works to use the `*` operator on a string, but I have to admit I can see no immediate practical application for `"Alice" * 5 = "AliceAliceAliceAliceAlice"`.

Variables are `initialized` the first time a value is stored, but they can be pointed to new values, which is called `overwriting`. Although PEP 8 says that underscores be used, camelcase is also completely acceptable for python to parse. More important is to be consistent within the entire codebase.

Comments in python are noted by a `#` (hashmark).

The `input()` function waits for a user to enter input before continuing. It should be assigned to a variable like so `myName = input()`. The `print()` function displays output to the terminal (or other interface) `print('It is good to meet you, ' + myName)`.

Length is abbreviated to `len()`. Starting to finally remember that one.

Data types are not implicitly cast to anything else under the hood (think js), so instead, there are functions to explicitly do that when it is wanted. `str(), int(), and float()`. However, integers and floating points can be compared to each other `42 == 42.0`

Booleans in python are spelled `True` and `False`.

Comparison operators work as expected. To compare equality is it `==`, there is no strict equal `===` as in javascript.

There are three boolean operators, `and`, `or`, and `not`, which, like in ruby, just flips the value.

### Code Blocks
Indentations matter as a way for the compiler to understand the code. A group of code is described as a `block`. A block of code begins when the identation increases, it can contain other blocks, and a block ends when the indentation decreases again.

An example from the docs to illustrate identations:
```py
  name = 'Mary'
  password = 'swordfish'
  if name == 'Mary':
    ➊ print('Hello, Mary')
       if password == 'swordfish':
        ➋ print('Access granted.')
       else:
        ➌ print('Wrong password.')

```

#### Flow Control and Notation
The standard cs concepts of flow control, such as if-else statements are available. Else if is written as `elif` The notation follows the indentation principle, but also adds a colon at the end, like so:
```py
if name == 'Alice':
    print('Hi, Alice.')
elif age < 12:
    print('You are not Alice, kiddo.')
else:
    print('Hello, stranger')
```

`while` loops also follow the colon notation and takes a condition that evaluates to True/False. While true, the loop continues to execute. `break` and `continue` are there to get out of it as well.

`for` loops work in conjunction with something that can be iterated, like `range()`
```py
for i in range(5):
    print('Jimmy Five Times (' + str(i) + ')')
```

And `range()` is super nice because it can take a single number, which becomes 0 to that number, or if passed two arguments, they become start and end (not inclusive):
```py
for i in range(12, 16):
    print(i)
```

And when passed a third, the `range()` can do an interval jump. If passed a negative number, it will step downwards, but make sure to have start and end numbers logical to that as well:
```py
for i in range(5, -1, -1):
    print(i)

# output:
# 5
# 4
# 3
# 2
# 1
# 0
```

### Modules
Although python has a basic set of functions built in like `str()`, `len()` and `input()`, it would be too bulky to include everything in the code set at once while running. So instead, code is broken off into `modules`, each of which contains a small bit of code relating to a logic domain, such as math. By importing just the additional functionality needed, programs are kept lightweight and efficient.

Importing a module follows the syntax of `import` followed by a comma separated list of modules. 

`import random, sys, os, math`
```py
import random
for i in range(5):
    print(random.randint(1, 10))
```

There is also an alternate syntax of `from random import *`, which in this use case is more verbose, but that star can be replaced by a method name if you want just the one.

### Exiting
Although a web server should never allow itself to terminate so simply, for scripts and smaller applications it can be super handy to end it early, before reaching the end of the code.
`sys.exit()`, but! you have to remember to import it where it is used as well `import sys`.