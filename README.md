# Sudoku Solver
 
## Introduction
Sudoku is a puzzle in which the objective is to find the suitable numbers from 1 through to 9 for each cell adhering to the rules of the game. There are four principal rules in the game (Sudoku Online, 2020):
 
1. Each row must contain numbers from 1 to 9 without any repetitions.
2. Each column must contain numbers from 1 to 9 without any repetitions.
3. There can be no repetitions in a single block/nonet
4. The sum of every single row, column and nonet must equal to 45, the entire solved puzzle must sum to 405.
 
> **Note:** Sudoku solvers are usually implemented to solve only solvable puzzles but for the purpose of this assignment, we also take impossible sudokus into account.

One way to go about solving sudoku is to try all combinations, while this certainly would work given the number of possibilities in sudoku this leads to over 6×10<sup>21</sup> possibilities. Hence, there are various algorithms which we can look at to solve it in a far shorter time.

 
## A simple backtracking algorithm
Initially, I implemented a backtracking algorithm which would recursively guess the value for each cell. The implementation was simple,
 
1. Find an empty cell to populate with a number from 1 to 9.
2. Verify no rules have been violated.
3. If so, move on to the next cell.
4. If yes, backtrack to the last entered number and try other numbers.  
5. Iterate through the implementation until the entire grid results in a total sum of 405.
 
While this solution was successful and was able to solve every solvable puzzle in under a mere second, the algorithm struggled with unsolvable puzzles given the excessively large problem space. To improve to this would be to reduce the problem space. 
 
## My solution
 
### Constraint Propagation
 
Constraint Propagation is a successful technique, where we describe the world in terms of decision variables that must be assigned values, we place explicit restriction on the values that are assigned henceforth. This leads to two assumptions about the problem (Kenneth, et al., 2006).
 
1. No uncertainty in the problem definition.
 
2. Problems are not dynamic.
 
Sudoku is a problem that respects both of these assumptions, given that the rules are definitive and the problem is dynamic. We can apply constraint propagation to sudoku to reduce our problem space as follows,
 
**Naive Approach** - Any empty cell in sudoku has the possibility of being a number from 1 through to 9.
 
**Sudoku as a constraint propagation problem** - Any empty cell in sudoku has the possibility of being a number from 1 through to 9 given that the same number is not on its row, column or its nonet.
 
The figure below demonstrates the drastic reduction in problem space offered via constraint propagation. The below example is only with one number on the board, with several numbers the possibilities reduce much further. 
 
![image info](Constraint.png)

# Improving Performance Further

The final implementation of my solver: The algorithm was further enhanced with 3 additional functions (``validRows`` , ``validColumns`` and ``validBoxes``) to check for invalid sudokus before trying to solve the puzzle. Then using constraint propogation to narrow the problem space (``constraintCheck``) and finally passing to an iterative function to perform depth first search and constraint propogation recusively (``search``). 

We can also use language-specific tools to optimize algorithmic performance. To implement the solution I have utilised a wide range of such tools including, using numpy, list comprehension, itertools and builtin functions such as ``sum``. 
 
## Performance Metrics
 
Both implementations were sufficiently fast, solving even hard solvable sudokus under a second. To benchmark performance of the algorithms I used two different inputs. All of the puzzles offered as a part of this task and also the "World's hardest Sudoku" known as "AI Escargot" (Stuart, 2008). 

```
[[8 0 0 0 0 0 0 0 0]
 [0 0 3 6 0 0 0 0 0] 
 [0 7 0 0 9 0 2 0 0] 
 [0 5 0 0 0 7 0 0 0] 
 [0 0 0 0 4 5 7 0 0] 
 [0 0 0 1 0 0 0 3 0] 
 [0 0 1 0 0 0 0 6 8] 
 [0 0 8 5 0 0 0 1 0] 
 [0 9 0 0 0 0 4 0 0]]
```

Below are some of the results that were gathered during testing.
 
| Problem   | Depth first search backtrack algorithm execution time (in s)  | Depth first search with backtracking and constraint propagation execution time (in s) |
| ----------- | ----------- | ------------------ |
| AI Escargot      | 2.178       |   1.038           |
| All Sudokus (provided with this task)   | < 600        |  8.610 |
 
The above results show a drastic difference given the inputs. The problem lies with the unsolvable sudokus, the minimized problem space tackles this exception quite well. The bigger problem size took significantly longer to execute was to sum the sudoku grid as a final check to be equal to 405.
 
## Future Works
 
### Strategies 

We can look further into reducing the problem space. In addition to constraint propagation, we can also utilize some other sudoku strategies. One such example is “Hidden Pairs”. A hidden pair occurs when a pair of numbers appears in exactly two squares in a row, column, or block, but those two numbers aren't the only ones in their squares.
 
![image info](https://www.sudokuwiki.org/PuzImages/HP1.png)
 
Source: https://www.sudokuwiki.org/PuzImages/HP1.png
 
In the above example, the 7 and 6 highlighted in green are a hidden pair. The 7 and 6 only occur in those two squares and nowhere else in the row, so those two squares can only contain 7 and 6 and no other numbers. Hence, we can eliminate other candidates in those squares, as highlighted in yellow. 
 
This is an example of a basic strategy, however more complex and often better strategies can be found on https://www.sudokuwiki.org. 
 
### Better algorithms 
 
Through further research I discovered more efficient algorithms that appear to solve sudoku. An algorithm that appears to work particularly well is through presenting sudoku as an **Exact Cover Problem** and solving it with **Donald Knuth's Algorithm X**. Exact cover is way of generalising a problem (such as sudoku) to solve it with algorithms such as Algorithm X to find all solutions (G, 2011).

## Bibliography

G, A., 2011. Solving Sudoku Revisited. [Online] 
Available at: https://gieseanw.wordpress.com/2011/06/16/solving-sudoku-revisited/
[Accessed 28 March 2022].

Kenneth, N., Brown & Miguel, I., 2006. Foundations of Artificial Intelligence. 2nd ed. s.l.:Elsevier.

Stuart, A., 2008. sudokuwiki.org/Escargot. [Online] 
Available at: https://www.sudokuwiki.org/Escargot
[Accessed 28 March 2022].

Sudoku Online, 2020. Sudoku Rules: Sudoku Online. [Online] 
Available at: https://www.sudokuonline.io/tips/sudoku-rules
[Accessed 28 March 2022].

