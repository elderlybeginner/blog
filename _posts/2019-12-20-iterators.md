---
layout: post
title: Learning Iterator Chains
date: 2019-12-20
tags: [Python, iterators, iterator chains, generator expression]
---

On my journey to understanding Python, I met **yield** keyword. Trying to grasp the idea of using it I start typing some code to generate similar effects, but with the knowledge I already have.

The point is to square values in given list and negate values in a given list. It is simple and I started with:

```python
# first approach: returning changed list
def sq(a):
    for i in range(len(a)):
        a[i] = a[i] * a[i]
    return a


def neg(a):
    for i in range(len(a)):
        a[i] = -a[i]
    return a


data = [1, 2, 3, 4, 5]

sqred = sq(data)
neged = neg(sqred)
```

It is not Pythonic, so let's see how yield works:

```python
# second approach: using iterator chain
def icsq(a):
    for i in a:
        yield i * i 


def icneg(a):
    for i in a:
        yield -i


data = [1, 2, 3, 4, 5]
icsqed = list(icsq(data))
icneged = list(icneg(icsqed))
```

It looks much better and... it's not Pythonic thou!

As I strongly believe that one day I will find a use for yield keyword it's not this time. As soon as I used *yield* I was confused and I felt I was missing something. That's my favorite sugar of Python:

```python
# third approach: using generator expression with ()
# list comprehension works as well and would be even better in this example
# as generator expression is not used as iterator

data = [1, 2, 3, 4, 5]

gesqed = list(x * x for x in data)
geneged = list(-x for x in gesqed)
```

It was mind exercise for me inspired by Dan Bader book [Python Tricks - 6.7 Iterator Chains](https://realpython.com/products/python-tricks-book/).

There was one more solution that came to my mind and I quickly typed a note to myself:
```python
# fourth approach: using decorator
# @wrapper is possible e.g. using it to extend sq function for negating,
# but it is against it's logic.
```

