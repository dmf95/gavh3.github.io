---
title: Demystifying the Python arrow notation.
date: 2021-09-13 18:25:00 -0700
categories: [Python]
tags: [python]     # TAG names should always be lowercase
image:
  src: /assets/img/comic-arrows.jpg
  width: 640   # in pixels
  height: 427   # in pixels
  alt: it's all virtual.
---
Occasionally I stumble upon something unusual but benign such that it warrants no more reaction than what's elicited through scrolling [r/hmmm](https://www.reddit.com/r/hmmm/).

Let me introduce the Python [function annotation](https://www.python.org/dev/peps/pep-3107/). Annotations are descriptions or "meta-data" in code to tell the reader what's going on. Conventionally, in-line comments do that job pretty well. For instance, this is how I would typically annotate a function:

```python:
def join_two_strings(string1, string2):
  '''
  Joins two strings and returns them as one.
  Args:
    string1 (str): first string
    string2 (str): second string
  Returns: str
  '''
  return string1 + string2
```

A few things to note:
- Each variable (input and output) has a specified datatype, but the function doesn't actually enforce that.
- Functionally, nothing changes from the Python interpreter's point of view if I remove the comments.
- The comments are there because I'm feeling nice.

Now, the points I mentioned are also applicable to function annotations, but the example would look like this instead:
```python:
def join_two_strings(string1: str, string2: str) -> str:
  return string1 + string2
```

In the above example, we introduce a few characteristics of function annotations. We tell the user what the function expects the data types of `string1` and `string2` are. Next, we use the arrow `->` to annotate the return result of this function, in this case it is a `str`. However, we are not limited to data types as annotations. A declaration like such is equally valid:

```python:
def join_two_strings(string1: "the first string", string2: "the second string") -> "joined string":
  return string1 + string2
```

When the code is run, Python ignores all of the annotations, hence they completely *optional*.

### So they're another way to comment my code.. Is that it?

Using function annotations opens up a special function attribute `__annotations__`. Printing the attributes will give us a dictionary mapping the annotations to each argument:

```python:
def join_two_strings(string1: str, string2: str) -> str:
  return string1 + string2
```
```
>>> print(join_two_strings.__annotations__)
Output: {string1: str, string2: str, return: str}
```

### How about optional arguments?
Let's change our function to accept a third, optional string.

```python:
def join_two_or_three_strings(string1: str, string2: str, string3: str = None) -> str:
  if string3:
    return string1 + string2 + string3
  else:
    return string1 + string2
```
```
>>> print(join_two_or_three_strings.__annotations__)
Output: {string1: str, string2: str, string3: str, return: str}
```