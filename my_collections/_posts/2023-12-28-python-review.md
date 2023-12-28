---
layout: post
title: Python Basics pt 2
category: dev
---

### Lists
`Lists`, or arrays as I got to know them, are an integral part of programming. A `list` contains `items`. They can be indexed in with bracket notation `my_list[0]`. A `slice` can be taken using bracket notation as well `spam[1:4]`, which goes up to but does not inlude the second index. If the first index is left out, it will start at the 0 index. Leaving both out copies the whole list. Regardless if part or all, slicing in this way always creates a new list.
```py
>>> spam = ['cat', 'bat', 'rat', 'elephant']
>>> spam[:2]
['cat', 'bat']
>>> spam[1:]
['bat', 'rat', 'elephant']
>>> spam[:]
['cat', 'bat', 'rat', 'elephant']
```
