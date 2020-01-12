---
layout: post
title: Sorting in Python (quick sort and selection sort) part 2 
date: 2020-01-05
tags: [Python, sorting, quick sort, selection sort, algorithms, recursion]
---

This is a follow up of the [first part](./sorting_in_python/). It's time to have some fun.

Let's do some tests in regards to the time that sorting takes for sorting n elements. From the results, I will try to confirm Big O times for a specific sorting.

First some modifications. This will create an array of: [100, 200, 300, ..., 2000] - it will be modified later on. 

```python
elements_arr = [x * 100 for x in range(1, 21)]
````

A loop for making different sizes of arrays/lists for testing.

```python
amount = 100
results = {}

print(elements_arr)
for elements in elements_arr:
	arr = [random.randint(0, elements) for x in range(elements)]
	ssort_time = timeit(ssort, arr, amount)
	ssort_loop_time = timeit(ssort_loop, arr, amount)
	ssort_loop2_time = timeit(ssort_loop2, arr, amount)
	qsort_time = timeit(qsort, arr, amount)
	sorted_time = timeit(sorted, arr, amount)
	results[elements] = [
		ssort_time, ssort_loop_time, ssort_loop2_time,
		qsort_time, sorted_time]
```

To print results let's use:

```python
print(f'\nTime in seconds for {amount} repetitions.')
print('-' * 50)
print('  amount   selecR   selec1   selec2   quickR   sorted')
for key, value in results.items():
	print(f'{key:8d}', *['{:8.2f}'.format(x) for x in value])
```

Interesting thing is that you can get:
> RecursionError: maximum recursion depth exceeded in comparison

It depends on which python shell you are using and probably different hardware and software factors have its influence. This is material for a different topic.

To cut off calculation above a certain limit, you can use:

```python
	if elements > 900:
		ssort_time = float("inf")
	else:
		ssort_time = timeit(ssort, arr, amount)
```

The results for sorting time:

> Time in seconds for 100 repetitions.
> --------------------------------------------------
>   amount   selecR   selec1   selec2   quickR   sorted
>      100     0.03     0.02     0.04     0.02     0.00
>      200     0.11     0.07     0.13     0.04     0.00
>      300     0.22     0.14     0.31     0.07     0.00
>      400     0.44     0.24     0.53     0.10     0.00
>      500     0.62     0.36     0.84     0.13     0.01
>      600     0.98     0.52     1.23     0.16     0.01
>      700     1.30     0.70     1.65     0.20     0.01
>      800     1.77     0.91     2.14     0.21     0.01
>      900     2.21     1.17     2.72     0.24     0.01
>     1000     2.77     1.39     3.41     0.27     0.01
>     1100     3.39     1.68     4.05     0.30     0.02
>     1200     4.15     2.02     4.78     0.34     0.02
>     1300     4.93     2.35     5.65     0.36     0.02
>     1400     5.66     2.69     6.73     0.41     0.02
>     1500     6.50     3.09     7.57     0.43     0.02
>     1600     7.54     3.57     8.55     0.47     0.02
>     1700     8.61     4.02     9.64     0.51     0.03
>     1800     9.74     4.50    10.80     0.53     0.03
>     1900    10.92     4.95    11.98     0.57     0.03
>     2000    12.22     5.53    13.25     0.59     0.03

Let's make one more test for quick sort and sorted():

> Time in seconds for 1 repetitions.
> --------------------------------------------------
>  amount   selecR   selec1   selec2   quickR   sorted
>  1000000      inf      inf      inf     7.01     0.45
>  2000000      inf      inf      inf    14.99     0.99
>  3000000      inf      inf      inf    23.93     1.58
>  4000000      inf      inf      inf    34.97     2.25
>  5000000      inf      inf      inf    47.82     2.87
>  6000000      inf      inf      inf    55.14     3.56
>  7000000      inf      inf      inf    65.29     4.04
>  8000000      inf      inf      inf    73.33     4.78
>  9000000      inf      inf      inf    86.75     5.55
> 10000000      inf      inf      inf    99.32     6.22
> 11000000      inf      inf      inf   109.00     6.98
> 12000000      inf      inf      inf   117.77     7.35
> 13000000      inf      inf      inf   121.13     7.83
> 14000000      inf      inf      inf   143.19     9.03
> 15000000      inf      inf      inf   154.89     9.88
> 16000000      inf      inf      inf   163.58    10.43
> 17000000      inf      inf      inf   183.80    11.32
> 18000000      inf      inf      inf   198.43    12.10
> 19000000      inf      inf      inf   207.76    12.99
> 20000000      inf      inf      inf   219.56    13.59

## Some observations while sorting

1. Only one core is working during sorting. This is expected as I did not "go into threads". Did sorted() worked the same way?

2. RAM using is going up with periodical jumps down as some memory is freed when some calculating line is cut off

3. When accidentally quick sorted an array/list with sorted elements quick sort gave longer times then selective sort. This is a confirmation of O(n^2^) theoretical sorting time for the worst-case scenario. How to dodge it is explained in [part one](./sorting_in_python/). The other issue is what to do if all elements are the same.

4. Quicksort also slowers when there are less unique values

5. Different shells allows different recursion level (eg. IPython goes deeper (wider) then IDLE))


## Saving results for future use

Let's save results for future use. It can be done with the following piece of code:

```python
import json

json = json.dumps(results)
f = open("results.json", "w")
f.write(json)
f.close()

print('')
f = open("results.txt", "w")
f.write(str(results))
f.close()
```

In the third part, I'm going to check how my results apply to the theory by drawing some charts.
