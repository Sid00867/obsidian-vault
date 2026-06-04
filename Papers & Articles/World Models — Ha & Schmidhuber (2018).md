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


"it’ll find a policy that looks good under our dynamics model, but will fail in the actual envi ronment, usually because it visits states where the model is wrong because they are away from the training distribution"

To make it more difficult for our C model to exploit defi ciencies of the M model, we chose to use the MDN-RNN as the dynamics model, which models the distribution of possible outcomes in the actual environment, rather than merely predicting a deterministic future. Even if the actual environment is deterministic, the MDN-RNN would in ef fect approximate it as a stochastic environment. This has the advantage of allowing us to train our C model inside a more stochastic version of any environment– we can simply adjust the temperature parameter τ to control the amount of randomness in the M model, hence controlling the tradeoff between realism and exploitability.

For instance, if we set the temperature parameter to a very low value of τ = 0.1, effectively training our C model with a M model that is almost identical to a deterministic LSTM, the monsters inside this dream environment fail to shoot fireballs, no matter what the agent does, due to mode collapse
![[Pasted image 20260604135004.png|530]]


> [!NOTE]
> An exciting research direction is to look at ways to incorporate artificial curiosity and intrinsic motivation (Schmidhu ber, 2010; 2006; 1991b; Pathak et al., 2017; Oudeyer et al., 2007) and information seeking (Schmidhuber et al., 1994; Gottlieb et al., 2013) abilities in an agent to encourage novel exploration (Lehman & Stanley, 2011). In particular, we can augment the reward function based on improvement in compression quality (Schmidhuber, 2010; 2006; 1991b; 2015a).

In the present approach, since M is a MDN-RNN that mod els a probability distribution for the next frame, if it does a poor job, then it means the agent has encountered parts of the world that it is not familiar with. Therefore we can adapt and reuse M’s training loss function to encourage curiosity.