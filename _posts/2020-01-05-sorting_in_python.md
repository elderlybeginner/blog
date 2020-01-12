---
layout: post
title: Sorting in Python (quick sort and selection sort) part 1 
date: 2020-01-05
tags: [Python, sorting, quick sort, selection sort, algorithms, recursion]
---

There are several sorting algorithms. Its effectiveness goes down to time complexity and space complexity. It's nicely shown on [Big-O Cheat Sheet website](https://www.bigocheatsheet.com). Big O notation is an interesting topic and it is always good to know the foundations.

## Selection Sort (non-recursive)

The idea is to choose the smallest element and put it in front. One way is to swap the smallest element with the first one and go through the whole list/array. The other way is to pop it out and append it to a new list/array.

Here is an example of the second way.

```python
def ssort(array):
	arr = array[:]
	new_arr = []
	while arr:
		new_arr.append(arr.pop(arr.index(min(arr))))
	return new_arr


arr = [3, 0, 2, 5, -1, 4, 1]

print("Sorted   array:", ssort(arr))
print("Original array:", arr)
```

## Selection Sort (non-recursive) with enumerate

I found another interesting solution on the internet. I don't like it, it's slower (well, selection sort is slow in general, so does it matter?) and language-specific.

```python
def ssort(arr):
	array = arr[:]
	for i, e in enumerate(array):
		mn = min(range(i, len(array)), key=array.__getitem__)
		array[i], array[mn] = array[mn], e
	return array


arr = [3, 0, 2, 5, -1, 4, 1]

print("Sorted   array:", ssort(arr))
print("Original array:", arr)
```

## Selection Sort (recursive)

In general, recursion is slower than "looping". It's harder to debug. It's harder to learn.  
On the other side, sometimes it's neat and elegant. You can see it below and you will see it in all its glory in quick sort recursive example. But first, let's go with the selection sort (recursive) solution.

```python
def ssort(arr):
	if len(arr) < 2:
		return arr
	i = arr.index(min(arr))
	return [arr[i]] + ssort(arr[:i] + arr[i + 1:])


arr = [3, 0, 2, 5, -1, 4, 1]

print("Sorted   array:", ssort(arr))
print("Original array:", arr)
```

Of topic here: what's more pythonic?

```python
	return [arr[i]] + ssort(arr[:i] + arr[i + 1:])
```

or

```python
	left, minimum, right = *arr, arr[i], *arr
	return [minimum] + left + right
```

## Quick Sort (recursive)

In its basics quick sort takes the first element of an array/list (pivot element) and puts a lower element on "one side" and bigger elements on "the other side". Then goes deeper with lower and bigger arrays/lists doing the same. The strategy is called "divide and conquer" and it deserves a separate post (or book).

To avoid *worst case scenario* such as a perfectly sorted array/list pivot element can be chosen randomly or the hole array/list can be mixed prior to sorting (not implemented in the code as it's needles for the example).

```python
def qsort(arr):
	if len(arr) < 2:
		return arr
	pivot, *rest = arr
	lo = [x for x in rest if x <= pivot]
	hi = [x for x in rest if x > pivot]
	return qsort(lo) + [pivot] + qsort(hi)


arr = [3, 0, 2, 5, -1, 4, 1]

print("Sorted   array:", qsort(arr))
print("Original array:", arr)
```

## sorted() built-in function/statement (Timsort)

Citing Wikipedia's entry:  
> Timsort is a hybrid stable sorting algorithm, derived from merge sort and insertion sort, designed to perform well on many kinds of real-world data. [^1]

Works the best, it's built-in... but it gives no fun of playing with sorting ;)

## Some fun with sorting random arrays/lists and time taking

Let's create random input data for sorting:

```python
import random

arr = [random.randint(0, 999) for x in range(1000)]

print("Random array:", arr)
```

I will also use some time taking function and each sorting will be executed "amount" of times to have some averaged results. Getting all together we have:

```python
#!/usr/bin/env python3

import random
import time


def ssort(arr):
	if len(arr) < 2:
		return arr
	i = arr.index(min(arr))
	return [arr[i]] + ssort(arr[:i] + arr[i + 1:])


def ssort_loop(array):
	arr = array[:]
	new_arr = []
	while arr:
		new_arr.append(arr.pop(arr.index(min(arr))))
	return new_arr


def ssort_loop2(arr):
	array = arr[:]
	for i, e in enumerate(array):
		mn = min(range(i, len(array)), key=array.__getitem__)
		array[i], array[mn] = array[mn], e
	return array


def qsort(arr):
	if len(arr) < 2:
		return arr
	pivot, *rest = arr
	lo = [x for x in rest if x <= pivot]
	hi = [x for x in rest if x > pivot]
	return qsort(lo) + [pivot] + qsort(hi)


def timeit(function, arg, amount):
	start_time = time.time()
	for _ in range(amount):
		function(arg)
	stop_time = time.time()
	return stop_time - start_time


def print_results(sort_type, time):
	print(
		f'{sort_type} sorting of {elements} elements {amount} times took',
		f'{time:.3f} seconds')


elements = 800
amount = 50
arr = [random.randint(0, elements) for x in range(elements)]
ssort_time = timeit(ssort, arr, amount)
ssort_loop_time = timeit(ssort_loop, arr, amount)
ssort_loop2_time = timeit(ssort_loop2, arr, amount)
qsort_time = timeit(qsort, arr, amount)
sorted_time = timeit(sorted, arr, amount)
print('')
print_results('Selection', ssort_time)
print_results('Selection (loop)', ssort_loop_time)
print_results('Selection (loop2)', ssort_loop2_time)
print_results('Quick', qsort_time)
print_results('sorted()', sorted_time)
```

The result is:

> ./sort.py 
> 
> Selection sorting of 800 elements 50 times took 0.836 seconds  
> Selection (loop) sorting of 800 elements 50 times took 0.456 seconds  
> Selection (loop2) sorting of 800 elements 50 times took 1.072 seconds  
> Quick sorting of 800 elements 50 times took 0.110 seconds  
> sorted() sorting of 800 elements 50 times took 0.005 seconds  

Some more testing, observations and conclusions can be found in the [next post](./sorting_in_python_2/).

[^1]: [Timsort](https://en.wikipedia.org/wiki/Timsort)
