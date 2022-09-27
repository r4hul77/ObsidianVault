A [[Monte Carlo Tree Search]] for dencentralized planning of robots with decentralized information gathering, Variational method and single robotic long term planning. #RobotPathPlanning [[Continous Envirnoments]], [[Multi-Robotic]]

## Problem Statement
Set of Robots $R=\{1,2,3,...R\}$ where each robot $r$ plans its own sequence of future actions $x^r=(x_1^r, x_2^r, ....)$ each action $x_j^r$ has a cost $c^r_j$ accociated with it. While each robot has a budjet $B^r$

Hence, we have our first constraint $$\sum C^r_j \le B^r \space \forall \space r \in R$$
So, at a time step $j$, next fessible actions are always a function of all the previous actions

$\mathcal{X}$ is set of all the fessible actions, $x$ is set of all the actions for all the robots, set of all the actions of all the robots but $r$ is  $x^{(r)} := x \setminus x^r$ simillary for $\mathcal{X}^r$.

All the Plans must reamin local, there could be comminication but non-reliable

## Algorithm Overview
Runs online in async form on all the robots it cycles in 3 states

