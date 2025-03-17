---
layout: post
title: Python Basics pt 2
category: python
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

The length of a list can be obtained by passing it to the `len()` method.

```py
>>> len(spam)
4
```

The item at any index can be updated by assigment.
```py
>>> spam[1] = 'aardvark'
>>> spam
['cat', 'aardvark', 'rat', 'elephant']
```

The `+` and `*` operators work on lists as well, similar to strings a pluls sign will append the two lists together, and the multiplier will copy the list and append to itself.

There is a `del` function that can unassign both simple variables and indexes in lists. In practice it is only really useful to delete from lists.

```py
>>> del spam[2]
>>> spam
['cat', 'rat', 'elephant']
```

Lists are probably one of the most common data types to work with. The `for item in <list>` will iterate over every item in the array. But often it is desirable to know which index the loop is iterating on, and so `len()` comes into play as well as `range()` to provide an index iterator:  

```py
for index in range(len(someList)):
  print('Index ' + str(i) + ' in someList is: ' + someList[i])
```

There are also a pair of operators to help with knowing if an item is in a list or not (curious why not something more like indexOf). `in` and `not in` return a boolean for a conditional.

```py
>>> spam = ['hello', 'hi', 'howdy', 'heyas']
>>> 'cat' in spam
False
>>> 'cat' not in spam
True
```

#### Tuple Unpacking
Tuple unpacking, aka multiple assignment, is a handy way to save some lines of code. As long as there is a variable for every value in the list, python can unpack it.
```py
>>> cat = ['fat', 'gray', 'loud']
>>> size, color, disposition = cat
```

This allows for a bit nicer of a way to iterate on a list and get both the index and item at once.
```py
for index, item in enumerate(supplies):
```

#### Randomicity in Lists
There is sometimes a need to randomly get one of the items from a list:
```py
>>> import random
>>> pets = ['Dog', 'Cat', 'Moose']
>>> random.choice(pets)
'Dog'
```

Or maybe even to just shuffle the whole thing in place:
```py
>>> random.shuffle(pets)
['Cat', 'Dog', 'Mouse']
```

#### Augmented Assignment
Augmented assignment is a shorthand to operate on a variable itself and save the new value to it.

| Augmented assignment statement | Equivalent assignment statement |
| ----- | ----- |
| spam += 1 | spam = spam + 1 |
| spam -= 1 | spam = spam - 1 |
| spam *= 1 | spam = spam * 1 |
| spam /= 1 | spam = spam / 1 |
| spam %= 1 | spam = spam % 1 |

`+` and `*` work for lists as well for concatenation and replication, respectively.

#### Methods vs Functions
Methods are similar to functions but are "called on" the item.  
`someList.index(item)` is like other languages and will find the index of the item, an important difference here is that a `ValueError: 'item' is not in list` error will be thrown if it doesn't exist. If duplicates in the list, the lower index will be returned.

Another handy one is `someList.append(item)`, which appends the item to the end of the list.

`someList.insert(indexInt, item)` will insert the item into the specified index, shifting the rest of the items back.

`someList.remove(item)` will remove only the first item in the list it finds, it will raise a `ValueError` if the item wasn't in the list to start with. The `del` statement is good to use when you know the index of the value you want to remove from the list. The `remove()` method is useful when you know the value you want to remove from the list.

`spam.reverse()` reverses the items of the list in place.

`someList.sort()` sorts numerically for ints/floats, asciibetical for strings;  and it can take a keyword argument (kwarg) to sort in reverse `someList.sort(reverse=True)`. It is not able to sort a list of mixed data types. Also, the sort is `ASCIIbetical order` rather than actual alphabetical order for sorting strings. This means uppercase letters come before lowercase letters. Therefore, the lowercase a is sorted so that it comes after the uppercase Z. `['Alice', 'Bob', 'Carol', 'ants', 'badgers', 'cats']`

To sort by normal alphabetical oder, sort takes a keyword argument to treat each item as lowercase, but it won't actually modify the list.
```py
>>> spam = ['a', 'z', 'A', 'Z']
>>> spam.sort(key=str.lower)
>>> spam
['a', 'A', 'z', 'Z']
```

> NOTE: These do not return the value of the new list as in some languages. They work `in-place` and return None.

### Line Continuation
`\` allows for code to run onto the next line if needed.

### Sequence Data Types
The Python sequence data types include lists, strings, range objects returned by range(), and tuples.

### Strings
The proper way to “mutate” a string is to use slicing and concatenation to build a new string by copying from parts of the old string. 