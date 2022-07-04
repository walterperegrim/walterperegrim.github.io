# An Overview Of Deep Reinforcement Learning

## Key Concepts & Terminology

### RL Core
#### states and observations
#### action spaces
#### policies
#### trajectories
#### value functions
#### Advantage Functions



### Dynamic Programming

#### Policy Evaluation

#### Policy Improvement

#### Policy Iteration

## RL Algorithm Taxonomy
![tax](https://spinningup.openai.com/en/latest/_images/rl_algorithms_9_15.svg))

### Model-Free RL
A model-free algorithm is an algorithm that estimates the optimal policy without using or estimating the dynamics (transition & reward functions) of the environment. In practice, a model-free algorithm either estimates a "value function" or the "policy" directly from experience (that is, the interaction between the agent and  environment), without using neither the transition function nor the reward function. A value function can be thought of as a function which evaluates a state (or an action taken in a state), for all states. From this value function, a policy can then be derived. 

#### Policy Gradient
In policy optimization methods the agent learns directly the policy function that maps state to action. The policy is determined without using a value function. Methods in this family optimize the parameters theta either directly by gradient ascent on the performance objective, or indirectly, by maximizing local approximations of. This optimization is almost always performed on-policy, which means that each update only uses data collected while acting according to the most recent version of the policy. Policy optimization also usually involves learning an approximator for the on-policy value function, which gets used in figuring out how to update the policy.

##### REINFORCE
The key idea underlying policy gradients is to push up the probabilities of actions that lead to higher return, and push down the probabilities of actions that lead to lower return, until you arrive at the optimal policy.
###### Quick Facts
VPG is an on-policy algorithm.\
VPG can be used for environments with either discrete or continuous action spaces.

##### PPO
PPO is motivated by the same question as TRPO: how can we take the biggest possible improvement step on a policy using the data we currently have, without stepping so far that we accidentally cause performance collapse? Where TRPO tries to solve this problem with a complex second-order method, PPO is a family of first-order methods that use a few other tricks to keep new policies close to old. PPO methods are significantly simpler to implement, and empirically seem to perform at least as well as TRPO. There are two primary variants of PPO: PPO-Penalty and PPO-Clip. \
PPO-Penalty approximately solves a KL-constrained update like TRPO, but penalizes the KL-divergence in the objective function instead of making it a hard constraint, and automatically adjusts the penalty coefficient over the course of training so that it’s scaled appropriately.\
PPO-Clip doesn’t have a KL-divergence term in the objective and doesn’t have a constraint at all. Instead relies on specialized clipping in the objective function to remove incentives for the new policy to get far from the old policy.
###### Quick Facts
PPO is an on-policy algorithm.\
PPO can be used for environments with either discrete or continuous action spaces.

##### SAC
Soft Actor Critic (SAC) is an algorithm that optimizes a stochastic policy in an off-policy way, forming a bridge between stochastic policy optimization and DDPG-style approaches. It isn’t a direct successor to TD3 (having been published roughly concurrently), but it incorporates the clipped double-Q trick, and due to the inherent stochasticity of the policy in SAC, it also winds up benefiting from something like target policy smoothing. A central feature of SAC is entropy regularization. The policy is trained to maximize a trade-off between expected return and entropy, a measure of randomness in the policy. This has a close connection to the exploration-exploitation trade-off: increasing entropy results in more exploration, which can accelerate learning later on. It can also prevent the policy from prematurely converging to a bad local optimum.
###### Quick Facts
SAC is an off-policy algorithm.\
The version of SAC implemented here can only be used for environments with continuous action spaces.\
An alternate version of SAC, which slightly changes the policy update rule, can be implemented to handle discrete action spaces.



#### Value Gradient
Q-learning learns the action-value function Q(s, a): how good to take an action at a particular state. Basically a scalar value is assigned over an action a given the state s.

##### DQN

##### SARSA

##### Rainbow

##### HRDQN



### Model-Based RL
Model-based RL has a strong influence from control theory, and the goal is to plan through an f(s,a) control function to choose the optimal actions. Thing of it as the RL field where the laws of physics are provided by the creator. The drawback of model-based methods is that although they have more assumptions and approximations on a given task, but may may be limited only to these specific types of tasks. There are two main approaches: learning the model or learn given the model.

## RL Algorithm Comparison

### Considerations When Choosing An Algorithm

#### Bias vs Variance

#### Sample efficiency

#### Stability & convergence

#### Generalization

#### Assumptions & approximation

#### Exploration vs Exploitation

#### Policy-centric v.s. Model-centric

#### Value-learning v.s. Policy Gradient

### Trade Offs

#### Policy Optimization vs Q-Learning
The primary strength of policy optimization methods is that they are principled, in the sense that you directly optimize for the thing you want. This tends to make them stable and reliable. By contrast, Q-learning methods only indirectly optimize for agent performance, by training Q_{\theta} to satisfy a self-consistency equation. There are many failure modes for this kind of learning, so it tends to be less stable. The primary strength of policy optimization methods is that they are principled, in the sense that you directly optimize for the thing you want. This tends to make them stable and reliable. By contrast, Q-learning methods only indirectly optimize for agent performance, by training Q_{\theta} to satisfy a self-consistency equation. There are many failure modes for this kind of learning, so it tends to be less stable.

#### model-free vs model-based
One of the most important branching points in an RL algorithm is the question of whether the agent has access to (or learns) a model of the environment. By a model of the environment, we mean a function which predicts state transitions and rewards.The main upside to having a model is that it allows the agent to plan by thinking ahead, seeing what would happen for a range of possible choices, and explicitly deciding between its options. Agents can then distill the results from planning ahead into a learned policy. A particularly famous example of this approach is AlphaZero. When this works, it can result in a substantial improvement in sample efficiency over methods that don’t have a model. The main downside is that a ground-truth model of the environment is usually not available to the agent. If an agent wants to use a model in this case, it has to learn the model purely from experience, which creates several challenges. The biggest challenge is that bias in the model can be exploited by the agent, resulting in an agent which performs well with respect to the learned model, but behaves sub-optimally (or super terribly) in the real environment. Model-learning is fundamentally hard, so even intense effort—being willing to throw lots of time and compute at it—can fail to pay off. Algorithms which use a model are called model-based methods, and those that don’t are called model-free. While model-free methods forego the potential gains in sample efficiency from using a model, they tend to be easier to implement and tune. As of the time of writing this introduction (September 2018), model-free methods are more popular and have been more extensively developed and tested than model-based methods.

