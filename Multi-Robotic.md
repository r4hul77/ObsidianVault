# Notes For Multi Robotic Systems


## Controls Techniques
1) Space Clustering (Conisder indivual robots into clusters get jacobians and formulate the probelm)

## Path Planning
1) Mixed Integer solvers
2) RRTs
3) Weight Graphs
4) Genetic Algorithms

## Taxonomy

### Collective Behaviour
1) Co-operative: Minimizing a common function 
2) Competitive: Against each other 

### Communication
1) Explicit: Robots use common communication media eg: Radios etc
2) Implicit: Robots infer information through the enviroment they are not communicating with each other

### Decision-making approach
1) Centralised: Central control agent with all the info must need communicate to robots. eg: easy to formulate, hard to scale
2) Decentralised: No central control agent- can hierarchical or distributed

### Problem Formualtion
- Discrette vs Continuous
- Known vs Unknown Goals: kown goal localition, unknown goal location
- Labelled vs Unlabelled : We don't know where each robot should go
- Coupled vs Decoupled: Coupled Huge Matrix for all the states whereas decoupled is robot takes care of itself.

## Decision-Making Approach

### Centralized
#### Coupled
- Planning in joint Configuration space
- For K robots: $$\mathcal{C}= \mathcal{C_1}\times\mathcal{C_2}\times\mathcal{C_3}...\times\mathcal{C_k}$$
- Use standard techniques to plan
- More robots more computationally harder problem

#### Decoupled
- Robots are planned seperately in their own space
- All these plans are instructed to the robot
- Local collision can be solved: Online or Offline
- This is non-optimal
- Co-ordination Strategies: Priority Schemes, Scheduling Schemes

### Decentralized Planning
- Information processed locally- its efficient computationally
- SubOptimal
- Implicit or Explicit Communication
- Coordination Strategies for collion avoidance. 1) local planner to replan

#### Dentralized Monte Carlo Tree Search
Decentralized [[Monte Carlo Tree Search]] w.r.t a beilf over the other agents future action sequences

### Hybrid
- Market Based Planning
