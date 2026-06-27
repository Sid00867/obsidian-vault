
[[Reading mat new q 3 v2]]


Given everything we've discussed over the past few days, I think you should stop trying to invent an entire new RL framework and instead look for a single missing capability. Here are directions I'd rank by tractability.

1. Adaptive Prediction Horizon (9/10)

This is where I'd start.

Current world models usually train with a fixed horizon:

one-step

k-step

rollout of fixed length


Question:

> Can the model learn when one-step prediction is sufficient and when long jumps are safe?



Examples:

Pong → predict 10 frames ahead.

Near paddle collision → predict every frame.


This doesn't require inventing new action spaces.


---

2. Learned Temporal Compression (9/10)

Instead of

s_t
↓

s_{t+1}
↓

s_{t+2}
↓

...

learn

s_t
↓

compressed transition

↓

s_{t+17}

Only if the skipped interval is predictable.

The question becomes:

> Which parts of trajectories deserve high temporal resolution?




---

3. Latent Actions (8.5/10)

Not "learn skills."

Instead ask

> Can action sequences be represented as latent variables that improve planning efficiency?



Benchmark:

Dreamer

MuZero

MiniGrid


Measure:

planning speed

sample efficiency



---

4. Adaptive Planning Resolution (8/10)

Imagine MPC.

Instead of

left
left
forward
forward
right

planner decides

Go around obstacle.

then expands only when necessary.

This is planning with variable resolution.

I don't think it's explored as thoroughly as variable planning depth.


---

5. Learned Planner Granularity (8/10)

Planner decides

Need detailed reasoning.

or

High-level reasoning is enough.

Almost like adaptive mesh refinement in numerical PDEs.


---

6. Multi-resolution World Models (7.5/10)

Instead of

one latent

learn

coarse latent

medium latent

fine latent

Planner queries whichever level it needs.


---

One question I think is underrated

This one stood out to me while reading your notes.

Instead of asking

> What should the abstraction be?



ask

> How does the agent know the current abstraction is failing?



That's a much cleaner research question.

Examples:

uncertainty increases

prediction error spikes

planner repeatedly replans

value estimates disagree


These become signals to "zoom in."

That immediately gives you an algorithmic problem.


---

Questions I would avoid

These are too big.

❌ Learn the optimal abstraction.

❌ Jointly learn state, action and temporal abstraction.

❌ General abstraction theory.

Those are thesis-level.


---

What I would do this summer

Spend a week reading papers in exactly this order:

1. Latent Actions (your instinct here is good)


2. Options / Skill Discovery


3. Adaptive Computation / Adaptive Depth


4. Temporal Abstraction in RL


5. Hierarchical World Models


6. Planning with Variable Horizon



For every paper, write down just one thing:

> What is fixed?



Examples:

Horizon is fixed.

Skill length is fixed.

Planner depth is fixed.

Latent resolution is fixed.

Action vocabulary is fixed.


After reading 20–30 papers, you'll likely notice that the same assumptions keep appearing. Those recurring fixed choices are often where research opportunities lie.

Of the ideas you've had so far, I think adaptive abstraction—particularly deciding when to plan or predict at different temporal and action resolutions—is the strongest long-term direction. The challenge now is not inventing a broader vision, but finding the smallest, testable piece of it that existing methods currently keep fixed.