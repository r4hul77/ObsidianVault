# PRM-RL

## Intro
Solution of #RobotPathPlanning by the use of [[Sampling Based Path Planning]] and [[Reinforcement Learning]]. The RL agent learns short point to point navigation. Sampling based planners provide roadmaps which connect the robot configurations that can be navigated by the RL-based agent.

##### Problems with Sampling based path planning
1) Must satisfy the constraints of the task
2) handle changes in the environment
4) Compenstate for sensor noise

##### Problems with RL
1) Hard to train with sparse rewards
2) Long range navigation is hard as it has sparse rewards causing them to be trapped

###### This Paper Idea
Use of RL agents as local planner(controller) and Sampling based planners for long range planning

## Methods
Works in 3 Stages
### 1) RL Training
The agent is trained in a simlar environment to deployment but with a very small state space to make the training more traceable ? . This stage is a monte Carlo Porcess. Multiple processes are trained and the fittest one is selected for stage 2

###### 1) Inputs

Start State $s$, Goal State $g$  are points in robots state space $S$ 

##### 2) Conditions

1) A state space point $x$ is vaild only if the constarints $L(x)$ as satisfied and points project $p(x)$ belongs in collision free points in configuration space.
2) The Task is said to complete if $||{p(x) - p(g)}|| \le \epsilon$

##### 3) Goal 

Is to find transfer funcition
$$\dot{x}= f(x, a)$$
In MDP setting Goal is find
$$\pi : S \rightarrow A$$

###### 4) State Space Info

1) Indoor Navigation: Polar co-ordinates w.r.t to goal state i.e $R^2$ and all the Lidar Observations i.e $R^{64}$ in $220\degree$ up to 5m so $x \in R^{66}$
2) Cargoo Delivery:  $x = [x_p, x_v, \eta, \dot{\eta}] \in R^{10}$ where $x_p = [x, y ,z]$ of quadcopter COM and $x_v$ are its velocity, $\eta = [\psi, \phi]$ of suspended mass and $\dot{\eta}$ are velocities

##### 5) Action Space

1) Indoor navigation: $a = [v_l, v_r] \in R^2$
2) Cargo Delivery: $a = [\ddot{x}, \ddot{y}, \ddot{z}] \in R^3$

##### 6) Transistion Probabilty

$P : S \times A \rightarrow R$
1) Indoor navigation: Simulator at 5Hz and $\mathcal{N}(0, 0.1)$
2) Cargo Delivery: Simulator at 50Hz similar $\mathcal{N}$

##### 7) Reward
For reaching the Goal in both the cases but in indoor env reward for keeping away from obstacles in case of cargo delivery minimizing the displacement of cargo

### 2) Road Map Creation
PRM builder is used to build roadmaps using RL agent as local planner 
![[PRM-RLAddedge.PNG]]

### 3) Road Map Querying
RL agent is used to execute the path, the agent may be task dependent but it is not environment dependent