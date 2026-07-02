
(arXiv:2602.00475)
## 1. Why do gradients vanish or explode?

Suppose a learned world model predicts the next state:

$$  
s_{t+1} = F_\theta(s_t, a_t)  
$$

If we roll the model forward for $T$ steps,

$$  
F_\theta^T(s_0, a)  
$$

represents the final state after repeatedly applying the model.

When optimizing the first action $a_0$, gradients must pass through every intermediate prediction. By the chain rule,

# $$  
D_{a_0}F_\theta^T

\left(  
\prod_{t=1}^{T}  
D_sF_\theta(s_t,a_t)  
\right)  
D_{a_0}F_\theta(s_0,a_0).  
$$

This is simply backpropagation through time.

The problem is that the Jacobians with respect to the state are multiplied together. Their singular values compound exponentially.

- Singular values $>1$ → exploding gradients.
    
- Singular values $<1$ → vanishing gradients.
    

As the planning horizon increases, optimization through the rollout becomes increasingly unstable.

---

## 2. Is this formulation new?

Not entirely.

Planning as optimization has existed for decades in control theory. Gradient-based trajectory optimization, Model Predictive Control (MPC), shooting methods, and direct collocation all optimize action sequences through dynamics models.

GRASP's novelty is **not** that it formulates planning as optimization.

Its contributions are instead:

- Lift intermediate states into optimization variables.
    
- Relax dynamics into soft constraints.
    
- Optimize actions and states jointly.
    
- Inject stochasticity into state optimization.
    
- Reduce the effect of long Jacobian chains.
    

In other words, it proposes a more stable optimization algorithm for long-horizon planning.

---

## 3. Does GRASP train the world model differently?

No.

This is an important distinction.

The world model is trained exactly as in previous work.

Typical pipeline:

```text
Collect data
    ↓
Train world model
    ↓
Freeze world model
    ↓
Run GRASP planner during inference
```

GRASP does **not** modify the training objective of the world model.

Instead, it changes **how planning is performed using a fixed world model**.

---

## 4. How is planning performed in GRASP?

Instead of only optimizing actions, GRASP also treats intermediate states as optimization variables.

Inference proceeds approximately as follows:

1. Start with:
    
    - initial state
        
    - goal state
        
    - initial action sequence
        
    - initial guesses for intermediate states
        
2. Compute a dynamics consistency loss that encourages the optimized states to satisfy the learned dynamics.
    
3. Optimize both:
    
    - actions
        
    - intermediate ("virtual") states
        
4. Add Gaussian noise to the states (Langevin updates) to encourage exploration and escape poor local minima.
    
5. Periodically synchronize with a true rollout through the world model so the optimized states remain physically consistent.
    
6. Return the optimized action sequence.
    

Unlike ordinary gradient planning, optimization is not forced to backpropagate through one long chain of Jacobians every iteration.

---

## 5. What does "imaginative planning" mean here?

The planner does not simply roll out one deterministic trajectory.

Instead, it maintains and optimizes a collection of intermediate states that can move independently while still being encouraged to satisfy the learned dynamics.

These virtual states act like imagined future configurations.

Noise allows the planner to explore different trajectories before converging to one that satisfies both:

- the learned dynamics, and
    
- the planning objective.
    

The imagination therefore comes from optimizing hypothetical future states rather than rigidly following a single rollout.

---

