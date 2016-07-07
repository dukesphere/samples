---
title: Tic-tac-toe
keywords: testDuke, retestDuke, etcDuke
last_updated: July 2, 2016
summary: "Sample explaining how to play tic-tac-toe"
sidebar: dukedocs_sidebar
permalink: /duke_tic_tac_toe/
---

Take turns in this 2-person board game to find out 
if you can get **_three in a row_** before your opponent
does. 

### Play space (tic-tac-toe board) {#playspace}

A square grid (table) composed three horizontal rows and three 
overlapping vertical columns to form nine cells. This is 
your tic-tac-toe board, where you play the game.

**Example (empty tic-tac-toe board):**

     ___ ___ ___
    |   |   |   |          
    |___|___|___|
    |   |   |   |
    |___|___|___|
    |   |   |   |
    |___|___|___|      

### Object of the game (how you win) {#winning}

Get three matching characters next to one another before your opponent 
does. Winning marks can be horizontal (across all three cells of one 
row), vertical (down all three cells of one column), or diagonal 
(descending from one cell at a top corner, through the middle cell, 
to the bottom corner cell on the other side of the grid). This is how 
you get "three in a row". 

**Examples of wins (_three in a row_):**

      ___ ___ ___      ___ ___ ___      ___ ___ ___
     | X | X | X |    | X | O | O |    | O |   | X |
     |___|___|___|    |___|___|___|    |___|___|___|            
     |   | O | O |    |   | O | X |    | O | X | X |
     |___|___|___|    |___|___|___|    |___|___|___|       
     | O | X | O |    | X | O | X |    | X | O | O |
     |___|___|___|    |___|___|___|    |___|___|___|
     
         X wins           O wins          X wins
       horizontally      vertically      diagonally

### Preparing to play {#preparation} 

* Provide a tic-tac-toe board. You might create your own 
board, for example, by drawing it on paper, using a stick 
to form it in sand, opening a spreadsheet, or even 
creating your own computer program. 
* Provide a writing tool for marking the cells in the tic-tac-toe 
board. You might choose a pen, stick, keyboard, or some other 
instrument for this purpose.
* Pick the player who will mark `X` characters and the player who  
will make `O` marks in the tic-tac-toe board cells. 
* Select the player who will put the first character on the board. 

### Understanding the rules {#rules} 

* This is a 2-person game.
* The tic-tac-toe board must be empty when the game starts: The cells 
must be empty. No `X` or `O` characters should be present on the board
when the game starts.
* One player must make `X` marks, the other `O` marks throughout a game. 
A player is not allowed to switch between using X's and O's in the 
middle of the game.
* Players must take turns, starting with the player who was selected 
to go first. (See ["Preparing to play"](#preparation).)
* The game ends when one player wins by getting _three in a row_ (see 
["Object of the game"](#winning) or when there is no longer a way to win 
because it is impossible to get _three in a row_ anymore.

**Example (no win possible):**

     ___ ___ ___
    | X | O | O |          
    |___|___|___|
    | O | X | X |
    |___|___|___|
    | X |   | O |
    |___|___|___|   

### To play the game {#gameplay}

1. Prepare to play if you have not done so already. 
(See ["Preparing to play"](#preparation).)
2. Learn the rules if you do not know them already. 
(See ["Understanding the rules"](#rules).)
3. Starting with the player selected to go first, take turns marking 
an empty cell on the board with the chosen character (`X` or `O`) 
until one player gets _three in a row_ to win or until it is no 
longer possible for anyone to win the game.
4. If you win, say "tic-tac-toe, three in a row," and draw a line that 
crosses through your winning set of `X` or `O` characters. 