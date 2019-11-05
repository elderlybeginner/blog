---
layout: post
title: Pythagorean Theorem - 'c' calculation in Python
date: 2019-11-01
tags: [Python, Pythagorean Theorem, mathematics, tricks]
---

How to calculate 'c'

This is one of the most remembered theorems:  
	a^2^ + b^2^ = c^2^

Here is uncommon and a dirty solution for c:

```python
c = abs(complex(a, b))
```

You can also go directly with:

```python
c = abs(a+bj)
```
