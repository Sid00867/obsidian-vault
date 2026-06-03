
MDP - A series of (S,A,R) tuples that follow the markovian property with transition dynamics

World model - probability of next state and reward conditioned on current state and action (a model of the world)

Model Based RL has world models while Model free doesnt

Model based RL uses world models to train/plan to take effective actions

Model free is a mapping over states and actions, no model in between


Policy Gradient Methods:

Policy gradient methods are fundamentally model free
They have a probability distribution over the actions space given the state space (basically the policy) and during training we concentrate our probability mass on favourable actions on a state. 

policy "gradient" just means how much to change the policy distribution (gradient) to achieve better reward maximizing policies

here we use something called a value function:
![[Pasted image 20260603154838.png]]

and:
do policy gradient methos use value funs? if so how? why need it

![[Pasted image 20260603155759.png]]



