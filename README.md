# 15 Puzzle Game

#### Formulation:
The game board consists of 4 * 4 grid with 15 tiles numbered from 0
to 15 in a randomized way. In each turn, the player can slide a tile into an adjacent empty space. Our job is to find a set of sliding moves of the blank tile which converts the initial board to the goal state.

## Abstraction

#### Intitial State:
Random arrangement of tiles from 0-15, 0 numbered tile being a blank tile

#### Goal State:
Tiles arranged in an ascending order from 1-15  with 0 at the last position of the grid.

#### State Space:
State of all objects are stored in the fringe. Each state object contains, the heuristic value of that node and an evaluation value i.e g(s) + h(s),  the path to the current state from the initial node.

#### Successor function
Successor function will give us the next possible states that can be generated by moving the blank tile. In this assignment, we have 3 Successor functions depending on the variant the users passes as an input
  1. Original: This Successor function generates successors of its neighboring tiles in all the direction of the current state, Up, down , left, bottom. We use check valid-index method to determine whether node exists specially in the case of edge nodes.
  2. Circular: In this variant, the successor function is defined same as original variant considering circular moves constraint.
  3. Luddy: Defined 8 moves with respect to the luddy constraint and successor can be found based on this moves.

#### Heuristic Function:
This heuristic function returns the number of misplaced tiles of current state. That is, it checks every tile of every game board to see if it is in goal-state. We first move the empty tile in all possible direction in the current state and calculate the h-score which is nothing but number of misplaced tiles. Then g-score is evaluated as number of nodes traversed from the start state to the current state. Example

#### Admissibility of the heuristic:
 We can say that the heuristic function is admissible because we are always underestimating the cost to reach the goal state, i.e. we cannot reach the goal state in fewer number of moves than the number of misplaced tiles in the board. Hence, each tile which is not in place must be moved at least once, this shows the admissibility.

#### Algorithm Used
The code was implemented using A* algorithm (Search 3 Algorithm)

#### Code Flow
The code takes two inputs one is board and other the variant. Then the code takes the initial-board as its first state as a start stage and finds the empty tile that is tile numbered 0. Depending on the variant the start state calculates all of its successor. Once the successors are calculated, it is added it to the closed set. Then for every successor we calculate the heuristic function and adds it to the priority queue. The node having the least heuristic value is returned or popped out of the queue. This process is repeated until we get the final state.

#### Approach & Problem Faced

The given code snippet was working only for original variant. Our next task was to make it work for two new variants circular and luddy respectively. Original variant was not giving a best solution as it did not take into account the visited state because of this some boards were running into an infinite loop.

We first of all implemented the visited state logic to remove the states that were already visited and then thought of implementing heuristic. There was some confusion in choosing heuristic, so this link quite helped me. https://cs.stackexchange.com/questions/37795/why-is-manhattan-distance-a-better-heuristic-for-15-puzzle-than-number-of-til

Pseudo Code for Heuristic: Number of Misplaced Tiles.

  for i in the state:

  if state[i] is not equal to i+1  
  #this will ensure all the nodes are in ascending order

      increment count
  return count
  #count will only increment if the two adjacent tiles are not in the ascending order

The next step was to implement priority queue to get the least value of the heuristic. Some state space was quite huge because of which our A* algorithm was not fast enough and consumed lots of time. To handle this case, I first of all thought may be using different heuristic could solve my problem at ease or perhaps it is due to heuristic I am getting large number of state space and traversing in the same loop. I tried using manhattan distance heuristic but was in the same loop hole of infinite loop and timeout error. Also read about IDA * search algorithm as it is the fastest solution to get the output. I tried implementing IDA * search but because the implementation was too complicated was not able to do so.

#### Code Run :
```
./solve_luddy.py [input-board-filename] [variant]

```

For Eg :

```
./solve_luddy.py board6 original

```
