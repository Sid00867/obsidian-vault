
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

one method - Monte carlo -> just repeatedly sample experiences and assign values based on rewards numerically. this is quite inaccurate sometimes because it fails to do TD learning, or the credit assignment problem, whereby it assigns bad values to all the actions in an experience, even tho only some might have contribuited to it. and you have to wait for the episode to end to assign values in MC too.

Differet ways to update Q in TD learning:
