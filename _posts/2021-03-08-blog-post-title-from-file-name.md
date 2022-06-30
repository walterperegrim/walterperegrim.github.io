## A Gentle Introduction Into Deep Reinforcement Learning

### Introduction


### RL Algorithm Taxonomy
#### model-free
A model-free algorithm is an algorithm that estimates the optimal policy without using or estimating the dynamics (transition & reward functions) of the environment.\ In practice, a model-free algorithm either estimates a "value function" or the "policy" directly from experience (that is, the interaction between the agent and \ environment), without using neither the transition function nor the reward function. A value function can be thought of as a function which evaluates a state (or an \ action taken in a state), for all states. From this value function, a policy can then be derived.

#### model-based

#### on-policy
#### off-policy

### RL Algorithm Tradeoffs
Sample efficiency — how many samples are needed to train a good policy?\
Stability & convergence — how easy & how fast the model converges.\
Generalization — Will the model generalize to other tasks?\
Assumptions & approximation — Does the method have any other constraints? Does the method work on discrete or continuous action space? What approximate is used?\
Exploration — How well does it explore the action space?\
Policy-centric vs Model-centric.\
Value-learning vs Policy Gradient\

### Selecting An Algorithm
