---
layout: post
title: Object beauty in Python 
date: 2019-11-24
tags: [Python, OOP, objects, functions]
---

Sometimes everything is a file[^linux]. Sometimes everything is an object[^python].  
The second one refers to Python. 

This post is not about OOP[^java], but about Python's idea of treating everything as an object. If we assume that **everything** is an object, then... function is an object as well. Thus, you can do with that function interesting things like storing it in data lists and can be iterable in a loop. That makes programming with functions very flexible.

```python
def yell(text):
    return text.upper() + '!' 


def reverse(text):
    return text[::-1]


do = [yell, str.capitalize, reverse]
print(do[0]('water, fire, earth, air'))

for func in do: 
    print(func('this is'), '.' * 15, f'{func.__name__}')
```

This example was based on "Python Tricks" by Dan Bader (3.1 Python's Functions Are First-Class). The book I am reading now and I can highly recommend. In this post, I only touched one thing that is written in 3.1 chapter of that book.

[^linux]: in Linux
[^python]: in Python
[^java]: Programming with objects is something different than treating something as an object. Here you have e.g. Java OOP (which is a beauty... not):
	
	```java
public class HelloWorld {

    public static void main(String[] args) {
        System.out.println("Hello, World");
    }

}
	```

