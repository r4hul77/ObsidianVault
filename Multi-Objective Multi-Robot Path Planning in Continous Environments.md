# Multi-Objective Multi-Robot Path Planning in Continous Environments
#RobotPathPlanning for [[Multi-Robotic]] Situations in an [[Continous Envirnoments]] using [[Artifical Potential Fields]] as A [[Genetic Algorithm]]. They are able to generate near-optimal solution for Path Planning
## Problem Defination
Problem of getting A robot from point A to B with out hitting anyting. Information availble is as follows:
- We know the free Space and Configuration Space
-  We Know the start postion and end position of the robot

### Evaluation
1) Length of the Path
2) Path smoothness
3) Path Safety

### Assumptions
1) Its a 2-D probelm
2) Robots are points and are inflatted by a radius to determine collision
3) Robots move at constant speed

## Algorithm
Its has two phases 
1) Find a Sub-Optimal intial solution using [[Artifical Potential Fields]] 
2) Improve it using [[Genetic Algorithm]]
### Environment Modeling
Usually continous space envirnoments are discrrettized to make them solved in real-time but these are limited by discretization size

Here the continous envirnoment in broken down into grids of nodes

### Artifical Potential Field
Highest potential is assigned to the Goal.

#### Initial Defs
Has 3 Lists OPEN, CLOSED, TEMP
- OPEN list has all the nodes which have to be explored
- TEMP has the nodes which have been explored but not all its children have not been
- CLOSED has the nodes which have been explored and their children have also been explored

#### Procedure
1) All the nodes are inserted into OPEN list
2) Destination node is removed from OPEN list , Largest potenital is added to it and it is added to TEMP List
3) All the nodes from thy obstacle nodes are removed and assigned a potential of -Largest potential and inserted into CLOSED List
4) From the Temp list the nodes is taken and its children are given nodes potenital - $\alpha$ , a small decrement
5) The explored node is added into CLOSED List
To determine the path, starting from the star of the robot next highest potenital node is selected and added to the path, if there exists 2 nodes with same potential the path is split. This creates enough initial paths for [[Genetic Algorithm]]. In case the paths generated are not enough for [[Genetic Algorithm]]. Random point are seletected from the path at a short radius and then added to the new path.
### Genetic Algorithm
These are the main features of the Algorithm
1) Varible length chromosomes to add more flexibity in finding the optimal path
2) Five arithemetic crossover and mutation operators to find optimal position of nodes.
3) An improvement Operator to reduce the number of nodes automatically if needed.
4) The GA is evolved untill a termination condition is meet
#### Selection Operators
They used Roulette Wheel Selection to select parents for cross over oeprator. Higher the quality better chances of generating offsprings and Rank Based Selection was also employed
#### Crossover Operators
###### Mean
$$x^f = \frac{x^{n}_1 + x^{n}_2}{2}, \space  y^f = \frac{y^{n}_1 + y^{n}_2}{2}$$
where $x^n_k, y^n_k$ are the all the node values for for parent k, Here its 1 and 2 not a orgy yet. If they are not of the same length then mean is between the smallest path's nodes and the ones in the largest node which are nearest to the node whose mean is to be calculated.
##### Random Crossover
$$x^f = \alpha x^{p}_1 + (1-\alpha)x^{p}_2, \space y^f = \alpha y^{p}_1 + (1-\alpha)y^{p}_2$$
Same nomenclature as above, same procedure as above $\alpha$ is a random vec of range $[-1,\space +1]$
#### Mutation operators
##### Random Direction
Changes the positons of node in random directions
##### Improve length and smoothness
$$\begin{align}x^f_i=x^p_i + \alpha(x^p_{i-1}-x^p_{i}) + \beta(x^p_{i+1}-x^p_{i})\\ y^f_i=y^p_i + \alpha(y^p_{i-1}-y^p_{i}) + \beta(y^p_{i+1}-y^p_{i})\end{align}$$
Used to improve the path and smoothness of a path

#### Deletion operators
Deletes the infessiable nodes before mating

#### Objective Function
$$S(p)=\sum_{i=1}^NA(l_{i-1}, l_i) $$
$$R(p)=\sum_{i=1}^{N-1}D_i$$
Where $S(p)$ and $R(p)$ are smoothness and safety of path p

$A(l_{i-1}, l_i)$ is change in direction to after following line $l_{i-1}$ to $l_{i}$ calculated using cosine rule

$D_i$ Distance from the closest obstacle

N number of piecewise line segments
$$C(p)=W_L\times L(P) + W_s \times S(P) + \frac{W_R}{R(P)} $$
all the $W_x$ are weights for each cost

## Multi Robot Path Planning
1) The optimal path for each robot should be consider with static obstacles
2) The optimal path should be checked for collisions among other robots
3) They should be modified based on collisions

To check for collisions the authors have two band aid fixes
1) They check the distance between all the robots at any given time and when they are less than a set distance from each other they have a function which is inversely propotional to the distance from each other and this is added as penatly 
2) One of the  collision path is selected and the collision point moved randomly

### Results and Discussion

They test it in 12 envirnoments
##### APF parameters
1) max_potential and $\alpha$ was selected such that -max_potential was always given to obstacles
2) Discretization size was always 1

##### GA parameters
1) Cross over and mulation probabilites were set to 0.35 and 0.15
2) Mutation rate (number of mutations efffected by mutation) was set to 0.2
3) Population size and number of iterations is direclty related to quality of the solution hence they evalate on various PSs and ISs

They ran their path planning algo 50 times mean for objective func and runtime was calculated

