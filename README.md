### Sudoku Solver

## Introduction 
Sudoku is puzzle in which the objective is to find the suitable numbers from 1 through to 9 for each cell not violating the rules of the game. There are four golden rules in the game: 

1. Each row must contain numbers from 1 to 9 without any repetitions. 
2. Each column must contain numbers from 1 to 9 without any repetitions.
3. There can be no repetitions in a single block/nonet
4. The sum of every single row, column and nonet must equal to 45, the entire solved puzzle must sum to 405.

---
**NOTE**

Sudoku solvers are usually implemented to solve only possible puzzles but for the purpose of this assignment, we also take impossible to solve sudokus into account. 

--- 

## Implementing Solutions
One way to go about solving sudoku is to try all combinations, while this certianly would work given the size and the possibilities of sudoku leads to over 6×1021 possiblities. Given the current computing power this certianly would take an astronomical amount of time. There are a various algorithms which to solve sudokus, some working more effiently than others. 

## A simple backtracking algorithm 
Initially, I implemented a backtracking algorithm which would recursively guess the value for each cell. The implementation was simple, find an empty cell to populate with a number from 1 to 9, verify no rules have been violated if so move on to the next cell if yes backtrack to the last entered number and try more numbers. Iterate though the implementation until the entire grid results to a total sum of 405. 

While this solution was successful and was able to solve every solvable puzzle in under a mere second. The algorithm struggled massively with unsolvable puzzles. 



## My solution 

# Constraint Propagation

Constraint Propagation (CP) is a succesful technique, where we describe the world in terms of decision variables that must be assigned values, we place explicit restricion on the values that are assigned henceforth. This leads to two assumptions about the problem. 

1. No uncertainty in the problem definition. 

2. Problems are not dynamic. 

Sudoku is a problem that respects both of these assumptions, given that the rules are definitive and the problem is dynamic. We can apply contraint Propagation to sudoku to reduce our problem space as follows, 

Naive Approach - Any empty cell in sudoku has the possibility of being a number from 1 through to 9. 

Sudoku as a CP problem - ANy empty cell in sudoku has the possiblity of being a number from 1 through to 9 given that the same number is not on its row, column or its nonet.

Expressing Sudoku as a CP problem reduces our problem space significantly. 


![image info](Constraint.png)


## Performance Metrics 

Both implementations were suffiently fast for the purpose of this assingment. 



## Future Works 




https://www.sciencedirect.com/topics/computer-science/constraint-programming
