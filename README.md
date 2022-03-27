### Sudoku Solver

## Introduction 
Sudoku is a puzzle in which the objective is to find the suitable numbers from 1 through to 9 for each cell adhering to the rules of the game. There are four golden rules in the game: 

1. Each row must contain numbers from 1 to 9 without any repetitions. 
2. Each column must contain numbers from 1 to 9 without any repetitions.
3. There can be no repetitions in a single block/nonet
4. The sum of every single row, column and nonet must equal to 45, the entire solved puzzle must sum to 405.

> **Note:** Sudoku solvers are usually implemented to solve only possible puzzles but for the purpose of this assignment, we also take impossible to solve sudokus into account. 

## Implementing Solutions
One way to go about solving sudoku is to try all combinations, while this certianly would work given the size and the possibilities of sudoku leads to over 6×10<sup>21</sup> possiblities. Given the current computing power this would take an astronomical amount of time. However, there are a various algorithms which to solve sudokus in a far shorter time. 

## A simple backtracking algorithm 
Initially, I implemented a backtracking algorithm which would recursively guess the value for each cell. The implementation was simple, 

1. Find an empty cell to populate with a number from 1 to 9.
2. Verify no rules have been violated. 
3. If so move on to the next cell. 
4. If yes, backtrack to the last entered number and try other numbers.  
5. Iterate though the implementation until the entire grid results to a total sum of 405. 

While this solution was successful and was able to solve every solvable puzzle in under a mere second. The algorithm struggled with unsolvable puzzles. As there are so many values to iterate over, to optimize this would be to  

## My solution 

# Constraint Propagation

Constraint Propagation is a succesful technique, where we describe the world in terms of decision variables that must be assigned values, we place explicit restricion on the values that are assigned henceforth. This leads to two assumptions about the problem. 

1. No uncertainty in the problem definition. 

2. Problems are not dynamic. 

Sudoku is a problem that respects both of these assumptions, given that the rules are definitive and the problem is dynamic. We can apply contraint propagation to sudoku to reduce our problem space as follows, 

**Naive Approach** - Any empty cell in sudoku has the possibility of being a number from 1 through to 9. 

**Sudoku as a constraint progragation problem** - Any empty cell in sudoku has the possiblity of being a number from 1 through to 9 given that the same number is not on its row, column or its nonet.

The figure below demonstrates the dramatic reduction in problem space offered via constraint propagation. 

![image info](Constraint.png)

## Performance Metrics 

Both implementations were suffiently fast for the purpose of this assingment, both algorithms solving hard solvable sudokus under a second. 

To measure the performance of algorithms I used different inputs. Below are some of the results that were gathered during testing.

| Problem   | Depth First Search Backtrack Algorithm Execution Time (in s)  | Depth First Search Backtracking with contraint propogation Execution Time (in s) |
| ----------- | ----------- | ------------------ |
| AI Escargot      | 2.178       |   1.038           |
| All Sudokus (provided with this task)   | < 600        |  8.610 |


The above results show a dramatic difference given the inputs. The problem lies with the unsolvable sudokus, the minimized problem space tackles this exception quite well. The bigger problem size took significantly longer to execute was to sum the sudoku grid as a final check to be equal to 405. 

# Optimizing algorithmic performance through lanaguge-specific tools

- Using numpy 
- Using list comphrension 
- Using itertools 
- Using builtin functions such as sum 

## Future Works 




https://www.sciencedirect.com/topics/computer-science/constraint-programming
