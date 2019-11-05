---
layout: post
title: Lambda function in Python
date: 2019-10-31
tags: lambda, function, Python 
---

I skipped lambda function several times when I was reading and learning Python. You have:

1. Regular def function e.g.:

```python
def plus(a, b):
	return(a + b)
```

2. Comprehensive lists e.g.:

```python
power = [x * x for x in range(10)]
```

So, what is lambda for?  
Well, I still don't know, but finally I read about it and I believe I have grasped how it works.

I'm telling myself that:

1. I'm assigning function to variable  
2. When I call lambda function/variable with an argument, this argument makes input before ':' and function give output after ':'

Looks like it works in my head. 

```python
>>> import math
>>> PI = math.pi
>>> sin_lambda = lambda x: math.sin(x*PI/180)
>>> cos_lambda = lambda y: math.cos(y*PI/180)
>>> type(sin_lambda)
<class 'function'>
>>> sin_lambda(0)
0.0
>>> sin_lambda(90)
1.0
>>> sin_lambda(30)
0.49999999999999994
```
