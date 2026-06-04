![[Pasted image 20260603225847.png]]

![[Pasted image 20260603225923.png]]

![[Pasted image 20260603230048.png]]

In our approach, we approximate p(z) as a mixture of Gaussian distribution, and train the RNN to output the probability distribution of the next latent vector z t+1 given the current and past information made available to it

![[Pasted image 20260603234743.png|626]]![[Pasted image 20260603234819.png]]
![[Pasted image 20260603234849.png]] ![[Pasted image 20260604000525.png]]

Furthermore, we see that in making these fast reflexive driving decisions during a car race, the agent does not need to plan ahead and roll out hypothetical scenarios of the future. Since ht contain information about the probability distribution of the future, the controller can just query the RNN instinctively to guide its action decisions.

We dont do planning nor imaginative training here. simply letting the controller have access to the model improves it

They have another experiment, vizdoom, where they do imaginative training:
![[Pasted image 20260604131710.png|492]]In this simulation, we do not need the V model to encode any real pixel frames during the hallucination process, so our agent will therefore only train entirely in a latent space environment. This has many advantages as we will see.
![[Pasted image 20260604131837.png]]

Introducing Artificial uncertainty TAU in dream envs makes better and robust policies
![[Pasted image 20260604132021.png|563]]

### 🌍 Key Idea

- A **world model** is an approximate probabilistic representation of the environment.
    
- Because it’s only an approximation, it sometimes generates **trajectories that don’t obey the real environment’s rules**.
    

### ⚖️ Example

- In the actual environment, the number of monsters in a room may differ from what the world model predicts.
    
- This is similar to how a child learns gravity but can still imagine superheroes flying — the model can produce unrealistic scenarios.
    

### 🎮 Implication

- The **controller (agent)** can exploit these unrealistic trajectories in the world model.
    
- However, such exploits may not exist in the **real environment**, meaning the agent might learn strategies that don’t transfer well.
