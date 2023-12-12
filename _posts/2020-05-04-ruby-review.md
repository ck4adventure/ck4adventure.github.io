---
layout: post
title: Ruby Review
date: 2020-05-04 14:27 -0700
categories: ruby rails how-to
---

Ruby Review

### File Execution

Running a file in ruby happens by putting this at the end

```
if __FILE__ == $PROGRAM_NAME
  # call your first function
end
```

## Pry REPL

REPL is any Read Eval Print Loop

Pry is a great way to be load in your ruby code and test each function independently.

Remember to quit pry with `quit`.

Check a stack trace after an error with `wtf`. Ahahaha.

## Byebug

Especially when you combine it with byebug to step into your code line by line and do other great debugging things.

Make sure to require byebug at the top of the file you'll be looking at.

Add the debugger keyword where you'd like it to stop and drop you in.

Step in `s`
Next line `n`
Continue `c`

Display your var each time you stop in the code with `display var`

Know what line of code it's on with `list=`

Conditional debug with `debugger if (val or expression)`. Single line, no end needed.

Use `back` or `where` to see the call stack trace.

Quit byebug with `exit`.