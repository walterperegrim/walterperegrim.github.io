# An Overview Of Deep Reinforcement Learning

## RL Algorithm Taxonomy
![tax](https://spinningup.openai.com/en/latest/_images/rl_algorithms_9_15.svg))

### Model-Free RL
A model-free algorithm is an algorithm that estimates the optimal policy without using or estimating the dynamics (transition & reward functions) of the environment. In practice, a model-free algorithm either estimates a "value function" or the "policy" directly from experience (that is, the interaction between the agent and  environment), without using neither the transition function nor the reward function. A value function can be thought of as a function which evaluates a state (or an action taken in a state), for all states. From this value function, a policy can then be derived. Two main approaches to represent agents with model-free reinforcement learning is Policy optimization and Q-learning.


#### Policy Optimization
In policy optimization methods the agent learns directly the policy function that maps state to action. The policy is determined without using a value function
Algorithms: REINFORCE, VPG, SARSA, PPO, TRPO

#### Q-learning
Q-learning learns the action-value function Q(s, a): how good to take an action at a particular state. Basically a scalar value is assigned over an action a given the state s.
Algorithms: Q-Learning, DQN, DDQN, DDPG, SAC


### Model-Based RL
Model-based RL has a strong influence from control theory, and the goal is to plan through an f(s,a) control function to choose the optimal actions. Thing of it as the RL field where the laws of physics are provided by the creator. The drawback of model-based methods is that although they have more assumptions and approximations on a given task, but may may be limited only to these specific types of tasks. There are two main approaches: learning the model or learn given the model.

#### Learn the Model
To learn the model a base policy is ran, like a random or any educated policy, while the trajectory is observed

#### Given the Model
I would say this had the “hypest” hype in recent time when AlphaGo Zero defeated the best go player in the world


### model-free vs model-based
One of the most important branching points in an RL algorithm is the question of whether the agent has access to (or learns) a model of the environment. By a model of the environment, we mean a function which predicts state transitions and rewards.The main upside to having a model is that it allows the agent to plan by thinking ahead, seeing what would happen for a range of possible choices, and explicitly deciding between its options. Agents can then distill the results from planning ahead into a learned policy. A particularly famous example of this approach is AlphaZero. When this works, it can result in a substantial improvement in sample efficiency over methods that don’t have a model. The main downside is that a ground-truth model of the environment is usually not available to the agent. If an agent wants to use a model in this case, it has to learn the model purely from experience, which creates several challenges. The biggest challenge is that bias in the model can be exploited by the agent, resulting in an agent which performs well with respect to the learned model, but behaves sub-optimally (or super terribly) in the real environment. Model-learning is fundamentally hard, so even intense effort—being willing to throw lots of time and compute at it—can fail to pay off. Algorithms which use a model are called model-based methods, and those that don’t are called model-free. While model-free methods forego the potential gains in sample efficiency from using a model, they tend to be easier to implement and tune. As of the time of writing this introduction (September 2018), model-free methods are more popular and have been more extensively developed and tested than model-based methods.


### Comparison Of Popular Libraries
