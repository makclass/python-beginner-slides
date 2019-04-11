# Python Basic Data Types

----

# Data Type

- Int
- Float
- String
- Boolean (True/False)
- None

----

# Collection Data Structure

- List
- Tuple
- Dictionary
- Set

----

# List

```python
sample_list = ["a","b","c","d"]
print(sample_list[-1])

for item in sample_list:
    print(item)
    
for i, item in enumerate(sample_list):
    print(i, item)
```

----

# Tuple

```python
sample_tuple = ('a', 'b', 'c')
a, b, c = sample_tuple
```

----

# Set

```python
sample_set = {'a', 'b', 'c', 'd'}
another_set = set([1,2,3,4,4,5,6,6,7])
```

----

# Dictionary

```python
sample_dict = {'name': 'Thomas', 'score': 65}
```

----

# Dictionary and List

```python
students = [
    {'name': 'Thomas', 'score': 65},
    {'name': 'Alan', 'score': 95},
    {'name': 'Jane', 'score': 85},
    {'name': 'Susan', 'score': 75},
    {'name': 'Chris', 'score': 45}
]
```

----

## List operations

- list.append(x)
- list.extend([1,2,3,4,5])
- list.insert(index, x)
- list.remove(x)
- list.index(x)
- list.pop()
- list.pop(index)
- list.clear()

----

# Check if an item is in the list

```python
if item in list:
    # Do something
````

----

# Check if an item is NOT in the list

```python
if item not in list:
    # Do something
````


----

# List Slicing

```python
sample_list = [1,2,3,4,5,6,7,8,9]
print(sample_list[0])
print(sample_list[-1])
print(sample_list[1:4])
print(sample_list[1:4:2])
print(sample_list[::2])
print(sample_list[:])
print(sample_list[:-5])
print(sample_list[-3:])
print(sample_list[::-1])
```

----

## Seeking Help

1. Using `__doc__`
2. Using `dir()`
3. Using `help()`

----

^__doc__

```
>>> sample_list.append.__doc__
'L.append(object) -> None -- append object to end'
```

----

^help

```
>>> help(sample_list.append)
Help on built-in function append:

append(...) method of builtins.list instance
    L.append(object) -> None -- append object to end
```

----

^dir

```
>>> dir(sample_list)
['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__iadd__', '__imul__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', '__rmul__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 'append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']
```

----

## Seeking Help Online

1. [Official Python Doc](https://docs.python.org)
2. [StackOverflow](https://stackoverflow.com)
3. [Geeks for Geeks](https://www.geeksforgeeks.org/python-programming-language/)

----

## Books

1. [Python Tips](https://book.pythontips.com)
2. [Automate the boring stuff with Python](https://automatetheboringstuff.com)
3. [The Hitchhiker’s Guide to Python](https://docs.python-guide.org)
4. [Python Crash Course](http://shop.oreilly.com/product/9781593276034.do)
3. [Python Data Science Handbook](https://jakevdp.github.io/PythonDataScienceHandbook/)

----

# Writing Comment

Comments are for human to read within programming code.

----

# Single line comment

```python
# Comment here
```

----

# Multi-lines comment

If one line of content is not enough, we can define multi-lines comments with three `"`:

```python
"""This is a multi-lines comments.

That accepts line breaks within the comment.
"""
```

----

# Doc String

- Multi-lines comment at the beginning is called Doc String.
- Doc String for a python file.
- Doc String for a function
- Doc String for a class definition.


