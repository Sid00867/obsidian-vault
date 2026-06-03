[122344.122377](https://dl.acm.org/doi/pdf/10.1145/122344.122377)

The essence of this architecture is basically:

-> There is a reactive policy mapping states to actions
-> There is a world model that tries to predict next state, rewards given current state and actions

Goal:

-> Learn the Reactive policy by RL with some experiences
-> Learn the world model with the same experiences (make world model predictions aligned with reality)
-> choose hypothetical (previous experiences) world state and action, use world model to imaginatively predict next state, further learn the policy by RL with this

RL method suggested by the paper -> Q learning

What hypothetical states to choose -> this is a planning problem

(action model here is the world model)

![[Pasted image 20260602225304.png]]![[Pasted image 20260602225328.png]]

Why learn imaginatively?

Faster rollouts and experiences, leading to faster convergence on optimal reactive policy.

==========

Planning method - IDP (Iterative Dynamic programming)


==**Problems with Dyna.**== 

IDP is too inefficient for large state spaces. (solved with later architectures)

> [!NOTE]
> Interesting Point -> Hierarchical Planning :
> Planning must be done at several levels, muscle twitches and a trip across the country require different wiring and mechanisms, and the results must be combined in some way.

![[Pasted image 20260602233228.png]]


Ambiguous and Hidden states (inherent stochasticity and uncertainty involved in state representation) -> maybe RSSM fixes it? idk
![[Pasted image 20260602233650.png]]

Incorporation of useful priors:
![[Pasted image 20260602234220.png]]