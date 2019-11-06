---
layout: post
title: Beginner's view on functional programming in Python
date: 2019-11-02
tags: [Python, functional, functional programming]
---

Let's go with the best to the worst:

1. *Comprehension lists* are simple, clear, powerful

Some examples:

Simple list:

```python
>>> [x for x in range(10)]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

Sinus dictionary table 0-90 degrees

```python
>>> import math
>>> PI = math.pi
>>> [{x: math.sin(PI * x / 180)} for x in range(91)]
[{0: 0.0}, {1: 0.01745240643728351},... # a lot of data
```

If statement gives even more functionality. This give common arguments from two lists:
 
```python
>>> a = [2, 3, 5, 8]
>>> b = [1, 2, 4, 7, 8]
>>> [x for x in a if x in b]
[2, 8]
```

And there are also nested comprehensive lists. Go check yourself.

[Official Tutorial - docs.python.org](https://docs.python.org/3/tutorial/datastructures.html#list-comprehensions)

2. *Recursive function* are clean, powerful and can be tricky

Most common examples are calculating factorial (n!) or Fibonacci numbers. You can find it easily.  
As a beginner I crashed system a few times as these recursion went out of control.

3. *Lambda Expressions* are useful, elegant.

Official Tutorial says it should be used when it helps with clarity. There is no point in pushing to use it. You feel it, you like it - you use it. Don't try to be too smart. Regular 'def name():' works good.

I had difficulties to understand lambda expressions. That helped me:

- you create lambda function by assigning it to variable (variable is the function),
- after *lambda* word is your input (x),
- after *:* is the output you want to get (your y in mathematics),
- you call you lambda with variable name and your input,
- in return you will get your output.

```python
hyper = lambda x: 1/x
```

```python
>>> hyper = lambda x: 1 / x
>>> hyper(2)
0.5
>>> hyper(50)
0.02
```

4. Magic *map()*, *filter()*, *reduce()* which are cumbersome.

Actually I don't understand them and I believe code looks more elegant with comprehensive lists or regular defs. As a beginner I consider this functions to be used by medium level programmers to show off. 
