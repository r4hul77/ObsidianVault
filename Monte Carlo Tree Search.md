MCTS Algorithims go about in steps.

#MDP #Search

Selection->Expansion->Simulation->Backup

## Selection
In this step we use policy to contruct a path from root to most promising leaf node (node with unexplored child nodes)

In case of AlphaGo, a UCB based policy is used each node has uscb value. One with highest value is selected 

$$UCB_i = \bar{x}_i + c\sqrt{ \frac{log N}{n_i}}$$

Where $\bar{x}_i$ is mean node value; $n_i$ number of visits; $N$ number of visits parent

We start from the start node untill a unexplored location is reached.

## Expansion
Here we randomly select a unexplored node

## Simulation or Roll Out
We just simulate the rest from this position with random states such that it is fast to execute.
![[14MilMeme.jpg | 300 | center]]
and set a reward to possible future

## Back Up

Now all the visted nodes present in the tree are updated with the rewards i.e there $\bar{x_i}$ is updated with some update rule


