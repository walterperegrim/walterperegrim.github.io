# A Gentle Introduction Into Deep Reinforcement Learning

## RL Algorithm Taxonomy

!([[https://mirrors.creativecommons.org/presskit/logos/cc.logo.svg](https://github.com/walterperegrim/walterperegrim.github.io/blob/main/_posts/rl-taxonomy.gv.svg)](https://github.com/walterperegrim/walterperegrim.github.io/blob/main/_posts/rl-taxonomy.gv.svg))

### Model-Free RL
A model-free algorithm is an algorithm that estimates the optimal policy without using or estimating the dynamics (transition & reward functions) of the environment.\ In practice, a model-free algorithm either estimates a "value function" or the "policy" directly from experience (that is, the interaction between the agent and \ environment), without using neither the transition function nor the reward function. A value function can be thought of as a function which evaluates a state (or an \ action taken in a state), for all states. From this value function, a policy can then be derived.\
SubClasses: Value Gradient, Policy Gradient

#### Policy Gradient (On-Policy)
An on-policy algorithm is an algorithm that, during training, chooses actions using a policy that is derived from the current estimate of the optimal policy, \ 
while the updates are also based on the current estimate of the optimal policy.\
Algorithms: REINFORCE, VPG, SARSA, PPO, TRPO

#### Value Gradient (Off-Policy)
An off-policy algorithm is an algorithm that, during training, uses a behaviour policy (that is, the policy it uses to select actions) that is different than the \ optimal policy it tries to estimate (the optimal policy).\
Algorithms: Q-Learning, DQN, DDQN, DDPG, SAC


### Model-Based RL
A model-based algorithm is an algorithm that uses the transition function (and the reward function) in order to estimate the optimal policy. The agent may have access \ only to an approximation of the transition function and reward functions, which can be learned by the agent while it interacts with the environment or it can be given \ to the agent (e.g. by another agent). In general, in a model-based algorithm, the agent can potentially predict the dynamics of the environment (during or after the \ learning phase), because it has an estimate of the transition function (and reward function). However, note that the transition and reward functions that the agent \ uses in order to improve its estimate of the optimal policy might just be approximations of the "true" functions. Hence, the optimal policy might never be found (because of these approximations).\
SubClasses: Pure Planning, Expert Iteration, & Policy Searching

#### Pure Planning, Expert Iteration, & Policy Searching
The most basic approach never explicitly represents the policy, and instead, uses pure planning techniques like model-predictive control (MPC) to select actions.\
In MPC, each time the agent observes the environment, it computes a plan which is optimal with respect to the model, where the plan describes all actions to take \ over some fixed window of time after the present. (Future rewards beyond the horizon may be considered by the planning algorithm through the use of a learned value \ function.) The agent then executes the first action of the plan, and immediately discards the rest of it. It computes a new plan each time it prepares to interact \ with the environment, to avoid using an action from a plan with a shorter-than-desired planning horizon.


### RL Algorithm Tradeoffs
Sample efficiency — how many samples are needed to train a good policy?\
Stability & convergence — how easy & how fast the model converges.\
Generalization — Will the model generalize to other tasks?\
Assumptions & approximation — Does the method have any other constraints? Does the method work on discrete or continuous action space? What approximate is used?\
Exploration — How well does it explore the action space?\
Policy-centric vs Model-centric.\
Value-learning vs Policy Gradient\

#### model-free vs model-based
A model-based learning agent uses knowledge of the environment dynamics in order to make predictions of expected outcomes. A model-free learning agent does not use such knowledge. The model here might be provided explicitly by the developer - that could be code for physics to predict a mechanical system, or it might be the rules of a board game that the agent is allowed to know and query to predict outcomes of actions before taking them. Models can also be learned statistically from experience, although that is harder to make effective.

#### on-policy vs off-policy
The primary strength of policy optimization methods is that they are principled, in the sense that you directly optimize for the thing you want. This tends to make \ them stable and reliable. By contrast, Q-learning methods only indirectly optimize for agent performance, by training Q_{\theta} to satisfy a self-consistency \ equation. There are many failure modes for this kind of learning, so it tends to be less stable. But, Q-learning methods gain the advantage of being substantially \ more sample efficient when they do work, because they can reuse data more effectively than policy optimization techniques. Serendipitously, policy optimization and \ Q-learning are not incompatible (and under some circumstances, equivalent), and there exist a range of algorithms that live in between the two extremes. Algorithms \ that live on this spectrum are able to carefully trade-off between the strengths and weaknesses of either side
