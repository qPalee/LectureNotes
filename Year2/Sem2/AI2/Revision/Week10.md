# Week 10

## Games
Game is a search problem
It is typically an <span style="color:#00bfff">Adversial Search</span> problem where your opponent has something to say about your strategy

There are many different types of games
#### Randomness
Deterministic - Tic-Tac-Toe, Chess
Shotastic - Poker, Mahjong

#### How many players
One - Solitaire, Puzzle Games
Two - Tic-Tac-Toe, Chess
Many - Poker, Mahjong

#### Are you playing against each other
Zero-sum - Tic-Tac-Toe, Chess
Non-zero-sum - Prisoner's Dilemma

#### Can you see the state
Perfect information - Tic-Tac-Toe, Chess
Imperfect information - Poker, Mahjong

#### Example - Tic Tac Toe
![[Pasted image 20240507103745.png]]

### Minimax
The minimax value of a node is the utility of the terminal state to which both players play optimally from that node

So the process of a two-player game is that one player maximises its utility whereas its opponent minimises the utility of max
#### Example
![[Pasted image 20240507103932.png]]

#### Complexity
Time complexity of $O(b^m)$, where b is the number of children a node may have and m is the max depth of the tree

Space complexity of $O(bm)$

### Alpha-Beta Pruning

#### Properties
- Pruning has no effect on minimax value for root
- Good child ordering improves effectiveness
- Full Search of many games (chess) is still hopeless