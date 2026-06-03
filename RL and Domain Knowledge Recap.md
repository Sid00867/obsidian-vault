
MDP - A series of (S,A,R) tuples that follow the markovian property with transition dynamics

World model - probability of next state and reward conditioned on current state and action (a model of the world)

Model Based RL has world models while Model free doesnt

Model based RL uses world models to train/plan to take effective actions

Model free is a mapping over states and actions, no model in between


Policy Gradient Methods:

Policy gradient methods are fundamentally model free
They have a probability distribution over the actions space given the state space (basically the policy) and during training we concentrate our probability mass on favourable actions on a state. 

policy "gradient" just means how much to change the policy distribution (gradient) to achieve better reward maximizing policies

here we use something called a value function, a baseline:
![[Pasted image 20260603154838.png|404]]

Policy gradient methods **can** use a value function, but they are not required to

1. Pure Policy Gradient (e.g., REINFORCE)

Pure policy gradient algorithms **do not use a value function**.

- **How it works:** They directly parameterize the policy (usually with a neural network) and learn by observing the actual total rewards (returns) from complete episodes. 
- **Drawback:** high variance

2. Policy Gradient with a Baseline (e.g., Vanilla Policy Gradient)

These methods incorporate a value function to make the learning process more stable.

- **How it works:** Instead of just using the raw reward, they subtract a state-value baseline (calculated by a learned value network) from the actual reward. This is called the **advantage function**.
- **Why it's used:** It reduces the variance of the gradient updates by answering "how much better was this action than average?"

3. Actor-Critic Methods (e.g., A3C, PPO, SAC)

These methods explicitly use **both** a policy and a value function.

- **The "Actor":** The policy network that learns to select actions.
- **The "Critic":** The value function network that evaluates the actions taken by the actor.
- **Why it's used:** The critic evaluates the expected returns, allowing the actor to update its policy continuously at every step, making it much more sample-efficient and stable. 


Note that we havent entered world models yet, these are all model free methods


![[Pasted image 20260603155759.png]]

State Value func (V) -> expected return following policy pi in state s
action value func (Q) -> expected return following policy pi in state s doing action a

note that these funcs by default have a policy function attached to them

### the state value function is just an averaged action value function over the actions.

![[Pasted image 20260603161732.png|397]]value funcs in bayesian RL & distributional RL -> how good a state is, but also how uncertain it is?

![[Pasted image 20260603162338.png|429]]

note that in (3) there is a cyclic dependency, Q depends on the policy, and the policy depends on Q to select action with highest value. as long as we improve 1, the policy improves
![[Pasted image 20260603163956.png|390]]
How to evaluate value funcs?

One method is **Monte Carlo (MC)**. It repeatedly samples experiences and assigns values based on the actual returns observed (the reward only and no bootstrapped value). For a state or state-action pair, we compute the total discounted reward obtained after visiting it and use that as the target value. A drawback is that you have to wait until the episode ends before assigning values. MC also tends to have high variance because the return can vary significantly between episodes, making learning unstable or slow.

**TD learning** solves this by bootstrapping. Instead of waiting for the full return, we come up with an estimate for every state-action pair relative to the estimate of another state-action pair in the next timestep, using one reward plus the next state's estimated value as the target. We do not need to explicitly compute all subsequent rewards in the episode. (Expressed as an equation below.)

For each transition, we observe the reward and next state, then update the current Q value toward the target formed by that reward and the next state's estimated Q value. We do this immediately at every timestep rather than waiting until the episode ends. Over many episodes, information about future rewards gradually propagates backwards through the state sequence as the Q estimates become more accurate. In this way, we can learn the Q function online while reducing the high variance associated with Monte Carlo methods.



The **value function is not what makes TD learning possible**. Rather, TD learning is possible because of **bootstrapping**.

The value function is simply what we're trying to estimate. Monte Carlo methods also estimate value functions.

The key difference is:

- **Monte Carlo:** update a value estimate using the actual return observed later.
- **TD:** update a value estimate using another value estimate.

In other words, TD learning relies on the fact that:

![[Pasted image 20260603192720.png]]

You could say:

> TD learning is possible because we maintain value estimates and bootstrap from them.

But if someone asked for the single concept that enables TD learning, the answer would be **bootstrapping**, not the value function itself. The value function is the object being learned; bootstrapping is the mechanism that learns it.




Different ways to update Q (value) in TD Model-free learning:
![[Pasted image 20260603193613.png]]
in other words, in any given state and action, MC is saying : what is my return?
SARSA is saying : how much better or worse is my return, relative to the new state and the action that i ended up taking?


note that expected sarsa takes consideration of all the possible actions in given state, as we can see that in plain sarsa the "next state term" in TD learning is just the one state from the episode we sampled, but many more future states are possible.

like the Q func, its possible for V too:
![[Pasted image 20260603193642.png|444]]

ON policy vs OFF policy: 
![[Pasted image 20260603195343.png]]so basically q learning chooses the optimal action value instead of what was actually chosen by the policy generating experiences. (like sarsa)

Nice piece of intuition -> even tho we dont have a world model, where if we take enough samples and do Q learning, Q will average out, and as we can see here, Q* will be approximately
estimate the expected value of the term we do our updates with.

the probability function of this expected term will be analagous to the world model, even tho we never really explicity built them.

meaning that even tho we dont have world model, the samples we collect will average out according to it.
![[Pasted image 20260603200506.png|621]]![[Pasted image 20260603201218.png|470]]

"If a series of state action pair trajectory is optimal, if we break it down then that should be optimal too"
![[Pasted image 20260603201349.png]]![[Pasted image 20260603201850.png|552]]

For Value Methods
![[Pasted image 20260603202021.png|516]]![[Pasted image 20260603202054.png|456]]

Continuous action use policy gradient methods.