---
layout: post
title: Tic-tac-toe - text game in Python with the game logic explanation
date: 2020-01-25
tags: [Python, game] 
---

Inspired by the book [Automate the Boring Stuff with Python](https://automatetheboringstuff.com/) I've started to "code" my own Tic-tac-toe game.

It's a text game and maybe I will add:

1. Tkinter version, to play it in a window
2. Flask or Pyramid version, to play it in a web browser

I'm going to describe some more interesting parts of the code now.

## The beginning

I started with an algorithm (or a diagram) on a sheet of paper. I was wondering if hand made drawing can help me to divide the game into smaller parts and visualize what I want to achieve. It worked surprisingly well. It helps a lot to understand the logic of the Tic-tac-toe game.

![algorithm](/assets/img/tictactoe.jpg)

## Data structure

One can choose lists (or list of list = matrix) or dictionary data structure to store and operate on "X" and "O". I went with different solution and XO are stored in a simple string of 9 elements.

## Make it easy to play

How about giving coordinates for a position where you want to place your 'X' or 'O'? No, it's cumbersome. Let's do it in a different way.

```python
def show_tips():
	print('\n\nUse 1-9 to play.')
	print('Just like Num keys')
	print('┌───┬───┬───┐' )
	print('│ 7 │ 8 │ 9 │')
	print('├───┼───┼───┤')
	print('│ 4 │ 5 │ 6 │')
	print('├───┼───┼───┤')
	print('│ 1 │ 2 │ 3 │')
	print('└───┴───┴───┘')
```

Unicode characters can be written with '\U2623' or copied or typed from an editor (in Vim:in insert mode: ctrl+v u2623).

## Input validation

Input is validated using try/except sentence and:

```python
if choice in '1 2 3 4 5 6 7 8 9':
	...
```

'choice' is a string typed by a user (by 'input'). This way only single character 1-9 is accepted.

## Result checking

How is the board? Someone won? Is it full (draw)? 
This is how to check board status.

```python
def check_result(board, mark):
	board_value = 0
	for i in range(9):
		if board[i] == mark:
			board_value += 2 ** i
	winning_board = [
		0b111000000,
		0b000111000,
		0b000000111,
		0b100100100,
		0b010010010,
		0b001001001,
		0b100010001,
		0b001010100]
	for b in winning_board:
		if b & board_value == b:
			return 'win'
	if ' ' in board:
		return 'not_finished'
	return 'draw'
```

I choose to check if the game is won by compering the board after each turn with the predefined winning board. The winning board is written with binary numbers for better visualization. As a whole board is a string of 9 characters, it is checked if e.g. board is 'XXX      '. To do that I transformed X or O on 0/1 and with Boolean 'and' ('&' in Python's syntax') I have checked if winning board and the board has the same bit's light-on. I guess it can sound complicated for many, although it's straightforward if you've been using binary and hexadecimal a lot.

## AI ;)

Let the computer play.  
I wish it could be a real AI. It's only a few rules.

1. Check if you can win now

First let's check indexes of empty positions:

```python
positions_to_check = [p for p, c in enumerate(board) if c == ' ']
```

Then, let's loop through all empty positions, one by one, using result checking.

2. Check if you should defend now

If I know I cannot win, I will check if I can stop my opponent from winning. This is checked the same way as above with a slight difference that I am executing the functions with the opponent mark.

3. Put the mark in the middle

The middle of the board is a safe place... providing that you are not starting with it and then you won't do something stupid. Play some games if you cannot grasp what I am talking about now.

4. Take an empty corner

5. Take anything that left

...and [the code](https://github.com/elderlybeginner/games/blob/master/tictactoe.py).

