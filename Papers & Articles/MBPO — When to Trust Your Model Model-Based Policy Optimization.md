👉 _Train the policy on shorter model rollouts branched from real data, instead of trusting long simulated trajectories._

That one design choice solves the biggest pain point in model-based RL: compounding model error.

### Why it matters

- **Long rollouts**: error accumulates, policies exploit model inaccuracies, performance collapses.
- **Short rollouts (1–5 steps)**: error stays bounded, synthetic data is still useful, and you get the sample efficiency benefits of model-based RL without instability.
- **Branching from real states**: ensures the synthetic data distribution stays close to what the model was trained on.

**Use your learned model conservatively — short bursts only — and you’ll get efficiency without sacrificing stability.**


why do we add synthesized branched data from real data when the real data is there?


The reason MBPO does this is **data amplification**:

- **Replay buffer limitation:** You only collect a limited number of real transitions per environment step. Training a policy and value function on just those can be slow.
    
- **Branching from real states:** By starting from _actual states_ in the buffer and rolling forward a few steps with the model, you generate _extra transitions_ that are close to the real distribution.
    
    - This avoids the “distribution drift” problem you’d get if you rolled out long trajectories entirely in the model.
        
    - The synthetic transitions enrich the dataset without straying too far from reality.
        
- **Why not just reuse real data?** Because the model can **fill in gaps**:
    
    - It can simulate what would happen under actions not taken in the real trajectory.
        
    - This gives the policy more diverse training signals than the environment alone provides.
        
    - In effect, you get more coverage of the state–action space without paying extra environment interaction cost.