# CLAR
CLAR is a novel Communication Learning mechanism of multi-Agent Reinforcement learning (CLAR) for heterogeneous scenarios. The above pictures shows algorithm and some experiment details for CLAR.

## Algorithm
The pseudo-code of the CLAR is presented in `Algorithm.png`. Line 5-23 illustrates the decentralized execution phase.  Next, Line 24-28 depicts the training procedure. During the decentralized execution proce-dure, the agents can communicate with others and se-lect actions in a decentralized manner according to the communication protocol. The trained heterogeneous graph attention network contains a set of learnable weights for each agent class. Due to the messaging nature of graph neural network updates, they can be distributed to individual agents during the execution pro-cedure. 
During the centralized training procedure, we as-sume that the MAGIC can receive the individual local observation-action histories from the replay buffer. The mixing network module is the same as that of QMIX, which takes the individual action-values as the input to perform monotone mixing and generates the global action-value .In addition, we leverage the loss function defined in QMIX to train the networks and update the parameters of networks.

## PCP
Predator-Capture-Prey consists of two types of cooperative agents, predators and captures, as shown in `PCP.png`. The target of the predator agent is to find the prey. At each time step, the state space of all predator agents is a concate-nation vector, which denotes the position of the agent and the information indicating the existence of prey, other predator agents or other capture agents. The dimension of action space of the predator agent is five and the action space of all agents is the same, which consists of action move down, move up, move left, move right and stay. The second type of agent, the capture agent, aims to locate and capture prey. The capture agent differs from the predator agent in both the action space and the observation space in that the capture agent does not obtain any observation in-puts from the environment. In addition, the capture agents have an additional action capture in their action space, and when they move to the location of the prey, they take the action capture to capture the prey located in the corresponding grid. Therefore, the target of the game is that all predators find a fixed prey, all captures find prey and then capture it. Each predator receives a -0.05 penalty per time-step until it accomplishes its per-class.


## SMAC
We evaluate it on the SMAC benchmark using pymarl framework which is open-source. We increase the difficulty of cooperation. On the one hand, we reduce the agent's range of sight from 9 to 2, and on the other hand, we choose challenging maps with compli-cated terrain as shown in `SMAC.png`.  In different combat scenarios, Ally units are all con-trolled by the reinforcement learning agents and enemy units are mastered by the built-in AI, whose level of dif-ficulty is set to medium. Enemy units and ally units can be asymmetrical, and their initial positions are random. The action space of the agent is of dimension four, which consists of actions move, noop, attack, and stop. Agents attack and move in these maps of continuous space under the control of these actions. At each time step, the agent receives a reward that is equivalent to the cumulative damage done to the enemy units. The agent can obtain an additional bonus of 10 for each enemy unit it kills and 200 for each battle it wins. We evaluate the proposed method on the three scenarios shown in `MAPS.png`, which provides brief descriptions of these scenarios.    

MMM2 is a super-hard scenarios, which contains Marines, Marauders, and Medivac. Each type of agents in these scenarios have their own unique attributes and skills. The ally agents succeed only when each agent performs to the best of its ability and coordinates the actions of other agents. Marauders have the high defense attribute, which can withstand more attacks from the enemy agents. Meanwhile, Marauders have slowing ability that can reduce the speed of enemy agents and pursue the enemy. Medivac has the healing ability that can provide treatment to the injured ally agents. Besides, Marines have the transportation ability that can withdraw ally agents from the battlefield. Marines have low-cost attribute thus they are suitable for mass production. To win the battle, Ally agents have to learn to communicate with other agents, such as sending their health situation to the Medivac.  

1o2r vs 4r scenario includes 1 Overseer and 2 Roaches of ally units. The target of the Overseer is to find the 4 Reapers of enemy units, and the gold of the 2 Roaches is to reach the positions of Reapers and try to defeat the Reapers. The Overseers and the Reapers are randomly generated in the scenario, and the enemy Roaches are randomly generated at other points. Considering that only the Overseers can get the information about the location of enemies, the Roaches must learn to aggregate the information of neighbor Overseers in order to win the battle effectively.  

2c3s5z scenario contains 2Colossus, 3Stalkers, and 5Zealots both for ally agents and enemy agents. Ally agents must learn many tactics, such as using Zealots to intercept enemy Zealots in order to protect Stalkers from serious damage. It is easier for agents to learn such strategies and coordinate actions under efficient information interaction.

## Hyper-parameters
`FIXED.png` describes the fixed parameters in all experimental scenarios, including their descriptions and fixed values. `PARAMETERS.png` shows the parameters of different experimental scenarios.
