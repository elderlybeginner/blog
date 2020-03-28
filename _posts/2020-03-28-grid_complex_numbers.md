---
layout: post
title: Use complex numbers as a grid (instead of a list of lists / string / matrix) 
date: 2020-03-28
tags: [Python, complex numbers, grid, matrix]
---

This is about game grids. This post is inspired by some problems I experienced when solving puzzles on [CodinGame](www.codingame.com).

Fighting with data that needs to modified or read made me looking for a better solution than storing grids as a list of lists.

The whole issue was inspired by simple question: how to simply adding two positions with X, Y coordinates.
	a = [3, 4]
	b = [4, 5]

As a beginner I wanted a + b = [7, 9], but instead of that, you can imagine ;), I got [3, 4, 4, 5].

Now, let's start from the beginning.

When you have a matrix build with rows and columns, there are a few data types you can use to build it and get access to cells depending on what you are going to store there.

Here are some solutions:

## List of strings

```python
rows = 4
columns = 8  # not used here

# a list of strings:
grid_ls = []

for y in range(rows):
	grid_ls.append('---..***')

print(*grid_ls, sep='\n')
print(grid_ls[3][6])
```

It works, however:
 - access to the grid is by double indexing ([y][x]),
 - changes are cumbersome as you have to split strings with:
	grid[y] = grid[y][0:a] + 'X' + grid[y][a:]
 - some relative movement is cumbersome. Just imagine that your are on position [x, y] and you would like to modify or read position in direction + a, + b (direction = [a, b]):
	cell = grid[position[0] + direction[0]][position[1] + direction[1]]

## List of lists

That's a pretty similar and most common way to access a matrix:

```python
rows = 4
columns = 8

# a list of lists:
grid_ll = [[0] * columns for x in range(rows)]  # A '*' can be insert directly here, if data in each row is the same

for y in range(rows):
	for x in range(columns):
		grid_ll[y][x] = '*'	

print(*grid_ll, sep='\n')
print(grid_ll[3][6])
```

It usually works a bit better than a list of strings when there are changes to be made as you don't have to split strings. The relative movement is still the same.

## Other common options

You can go with a matrix in 'import pandas' or you can create a class and an object.
That's overpower for me.

## Complex numbers - ultimate solution

There is another very neat and simple solution. You can use complex numbers which in its nature already consist of two axes. I was reluctant at the beginning to use it. That was a mistake. Here is how easy it is to work with it.

```python
rows = 4
columns = 8

# a dictionary with complex numbers

grid_cn = {} 

for y in range(rows):
	for x in range(columns):
		grid_cn[x + y * 1j] = '*'	

print(*grid_cn.values())
print(grid_cn[6 + 3j])
```

Where is the gain?

	a = 3 + 4 * 1j
	b = 4 + 5 * 1j

	a + b = 7 + 9 * 1j

Thus, it's much easier to operate when coordinates are complex numbers:

	cell = grid[position + direction]
	
[Pirate's treasure](https://www.codingame.com/ide/puzzle/pirates-treasure) is a good place to try it in practice.
