[122344.122377](https://dl.acm.org/doi/pdf/10.1145/122344.122377)

The essence of this architecture is basically:

-> There is a reactive policy mapping states to actions
-> There is a world model that tries to predict next state, rewards given current state and actions

Goal:

-> Learn the Reactive policy by RL with some experiences
-> Learn the world model with the same experiences (make world model predictions aligned with reality)
-> choose hypothetical world state and action, use world model to imaginatively predict next state, further learn the policy by RL with this

(action model here is the world model)

![[Pasted image 20260602225304.png]]![[Pasted image 20260602225328.png]]
