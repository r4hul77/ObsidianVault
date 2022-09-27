# Graph Neuralnes for decentrailized planning

#RobotPathPlanning [[Multi-Robotic]] #Decentralized #NeuralNetworks #DeepLearning #GraphNeuralNetworks

The authors suggest an commbiend arch. Where a CNNs learns on local features and a GNN learns on communication between robots, CNN that extracts local features and GNN communicates them. These networks are trained offline on a coupled planner and are ran online on the robots in decoupled and decentalzied fasion. They also have a online planner which solves the conficts thus improving training time.

##### Contributions
- Information is shared over a ***multi-hop communication network**,* through explicit communication with nearby  neighbours only
- They only have local relative information only so no global refrence frame

##### Works on Decentralized System
