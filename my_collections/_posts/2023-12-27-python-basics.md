---
layout: post
title: Python Basics
category: dev
---

I just came across what I think is a great book on Python called [Automate The Boring Stuff](https://automatetheboringstuff.com/2e/chapter1/) and so I thought I'd write up some notes as I read it, not because I don't understand basic programming, but because I don't always talk about programming with others, so a refresher in the *nomenclature* is important to me, as well as understanding some of the nuances of Python.

The first thing (which I think I had learned once and forgotten) was that Python is not named for the snake, but for the comedy troupe. 

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