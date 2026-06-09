### Core Research Question

> **Can a learned world model improve decision-making by explicitly modeling its own properties (uncertainty, competence, learning progress, and blind spots), rather than only modeling the external environment?**

---

### More Concrete Version

> **What information about a world model is useful for policy improvement, and can an agent learn a self-model that adaptively guides exploration and planning?**

---

### First Experimental Question

> **Does giving a policy access to a learned representation of its world model's uncertainty and learning dynamics improve exploration compared to standard exploration methods?**

This is probably the cleanest place to start.

---

## Reading List

### 1. World Models (Foundation)

1. World Models
2. Dream to Control
3. Mastering Diverse Domains through World Models

**Goal:** Understand what information is already present inside learned latent world models.

---

### 2. Curiosity & Exploration

4. Curiosity-driven Exploration by Self-supervised Prediction
5. Plan2Explore

**Goal:** Learn how agents currently estimate "I don't know this."

---

### 3. Uncertainty Estimation

6. Deep Exploration via Bootstrapped DQN
7. Simple and Scalable Predictive Uncertainty Estimation using Deep Ensembles

**Goal:** Understand epistemic uncertainty and model confidence.

---

### 4. Meta-Learning

8. RL²: Fast Reinforcement Learning via Slow Reinforcement Learning
9. Learning to Reinforcement Learn

**Goal:** Understand how agents can learn properties of their own learning process.

---

### 5. Metacognition / Self-Modeling

10. A Survey of Confidence Estimation and Calibration
11. Literature on:

- metacognition in AI
- self-reflective agents
- introspective neural networks
- calibrated decision making

**Goal:** Understand how an agent can reason about itself rather than the environment.

---

## Suggested Reading Order

1. World Models (Ha & Schmidhuber)
2. DreamerV3
3. Plan2Explore
4. RL²
5. Learning to Reinforcement Learn
6. Bootstrapped DQN
7. Deep Ensembles
8. Calibration / Metacognition papers

---

### The Underlying Scientific Question

After stripping away all implementation details, the deepest version of the idea is:

> **Should intelligent agents maintain models of themselves in the same way they maintain models of the external world, and what computational advantages emerge when they do?**

That's the question I'd keep pinned above your desk while reading. Everything else is an attempt to make that question experimentally tractable.

================

| **Paper / Framework**                                          | **Core Mechanism**                                                                                       | **Relevance to Your Idea**                                                 |
| -------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| **Plan2Explore** (Sekar et al.)                                | Uses an ensemble of novelty-seeking transition models to plan for maximum expected misalignment.         | Best baseline for "seeking out blind spots."                               |
| **MOPO / COMBO**                                               | Pessimistic offline MBRL that penalizes rewards based on model uncertainty.                              | Standard framework for how uncertainty alters decision-making.             |
| **World Action Verifier (WAV)** _(Recent 2026 Work)_           | Decomposes state prediction into plausibility and action reachability to self-verify.                    | Cutting-edge example of a world model assessing its own structural limits. |
| **Pathways to AGI Survey / LeCun's Configurator Architecture** | Proposes hierarchical world models containing an explicit "cost/energy" module assessing self-alignment. | Conceptual framework for self-reflective AI agents.                        |


Do not frame it generally as "using uncertainty for exploration or safety." Instead, frame it as **Structural Metacognition in World Models**—designing an architecture where the world model treats its own learning constraints and epistemic boundaries as core internal states to be predicted alongside environmental transitions, eliminating the need for bulky ensembles or simplistic heuristic penalties.

## Why a Parallel Self-Model "Improves" Learning

In a standard world model (like DreamerV3), if an agent fails to predict an outcome, it treats it as an environmental error. It doesn't understand _why_ it failed. Separating the two models gives the agent a "Theory of Mind" applied to itself, unlocking three major capabilities:

### 1. Intent Preservation Over Distraction (Intentions)

- **The Standard Way:** If an agent is playing a game and gets knocked off course by a random obstacle, its policy must recalculate based entirely on the new environmental state.
    
- **The Self-Model Way:** The Self-Model tracks a persistent latent vector representing the agent's _active goal or intention_. Even if the environment changes drastically, the internal "intention vector" remains stable, allowing the agent to resume its original plan smoothly. It decouples _what I want to do_ from _what the environment is doing to me_.
    

### 2. Disentangling "My Body" from "The World" (Dangers & Blind Spots)

- **The Standard Way:** If a robot's motor degrades or its camera gets smudged, a traditional world model thinks the physics of the _universe_ changed. It has to completely retrain its transition dynamics.
    
- **The Self-Model Way:** Pioneered by researchers like Hod Lipson (_"Task-agnostic self-modeling machines"_), a dedicated self-model simulates the robot’s own physical and functional boundaries. If a motor fails, the Self-Model updates its internal "competence map" instantly. The agent realizes, _"The world is the same, but my capability has shrunk,"_ allowing it to adapt safely without breaking its understanding of external physics.
    

### 3. Intentional Focus Control (Curiosity)

- **The Standard Way:** The agent explores based on pixel-level prediction errors. If a television screen in the environment is flashing random noise, the agent gets stuck staring at it forever (the "Noisy TV problem") because the prediction error is always high.
    
- **The Self-Model Way:** The Self-Model tracks the agent's _own learning trajectory_. It notices, _"I have been staring at this TV for 100 steps, and my internal uncertainty is not decreasing."_ By recognizing its own lack of learning progress, it flags the area as an unlearnable blind spot and forces the agent to move on.
    

## The Core Structural Challenge (Your Research Angle)

If you want to pursue this, the open research question isn't _whether_ this helps (intuitively, it does), but **how the two models interact.** In humans, our self-model and world model are deeply intertwined. If you want to build this computationally, you have to design the bridge between them:

```
[Environment] --------> [ World Model ] ---\
                                            ---> [ Shared Latent Space ] ---> [ Policy / Planning ]
[Internal Signals] ---> [  Self-Model  ] ---/
```

### How to frame your novelty:

Instead of building a monolithic neural network, you can propose a **Split-Latent World Model Architecture**.

- **Model A (The Physics Engine):** Predicts $P(s_{env}' \mid s_{env}, a)$.
    
- **Model B (The Metacognitive Engine):** Predicts $P(s_{self}' \mid s_{self}, s_{env}, a)$.
    

You then force the policy to plan using a joint representation of both. During imagination rollouts, the agent wouldn't just simulate what the environment will look like; it would simulate how its own internal states (confidence, intent preservation, risk) fluctuate across those future steps.

## Verdict & Next Steps

This is absolutely worth pursuing. It addresses a major flaw in current MBRL: the lack of structural ego-centric awareness.

To ground this in existing literature so you can find your specific gap, look up:

1. **"Task-agnostic self-modeling machines" (Kwiatkowski & Lipson)** – Great for tracking physical self-properties.
    
2. **"Modeling the Mental World for Embodied AI"** – Explores structuring internal mental states vs. physical world attributes.
    
3. **Metacognitive Reinforcement Learning (MCRL)** – The mathematical framework for agents evaluating their own internal components.
    

What specific domain are you thinking of testing this dual-m


-==================

## 1. Why Couple Both Latent States?

If Model A (World) and Model B (Self) run entirely in parallel without their latent spaces interacting, the agent becomes structurally fragmented. It would be like a human who understands the physics of a car and understands their own fear, but cannot connect the two to realize, _"I am afraid because this car is moving too fast for my current reaction time."_

Coupling the latent states creates a **functional bridge** that yields three massive advantages:

### Contextual Competence Mapping

The Self-Model needs to know what the environment looks like to evaluate its own capabilities. For example, your self-model's estimation of your "balance competence" changes drastically depending on whether Model A predicts you are walking on concrete or ice. The latent state of Model B ($z_{self}$) must be conditioned on the latent state of Model A ($z_{world}$) to make context-aware self-predictions.

### Grounding Intentions in Reality

If the Self-Model maintains an internal "intention" or goal state, that intention has to be projected onto the world model to plan actions. If your intention is to "find water," your planning mechanism needs to cross-reference that internal state with the world model's map to look for rivers or wells.

### Unified Imagined Rollouts

During imagination-based planning (like in Dreamer), the agent projects the future forward step-by-step in its head. By coupling the latent states, the agent can simulate how a physical change in the world smoothly triggers a psychological or functional change in itself.

## 2. Preventing Model B from Becoming a Copy of Model A

If you train both models on the standard end-to-end RL loss (maximizing reward or minimizing total reconstruction error), **Model B will just cheat.** It will use its capacity to help Model A reconstruct pixels because predicting the environment is a massive, high-entropy task. This is called **representation collapse**.

To prevent this and enforce a strict separation of duties, you must use **Information Bottlenecks**, **Asymmetric Gradients**, and **Distinct Reconstruction Objectives**.

### Mechanism I: The Asymmetric Gradient Wall (Stop-Gradient)

You must structurally prevent Model B from helping Model A predict the environment. You do this by placing a `stop_gradient` operation on the channel flowing from Model B to Model A.

- **How it works:** Model B can look at Model A's features to understand the context of the world. However, during backpropagation, gradients from the world-prediction loss (predicting pixels, rewards, or next states) **cannot** flow back into Model B.
    
- **The Result:** Model B is completely useless for predicting the external world, forcing it to find something else to optimize.
    

### Mechanism II: Distinct Informational Objectives

You must feed Model B a completely different target signal than Model A. While Model A tries to predict external sensory data ($s_{t+1}$), Model B is trained to predict **internal metacognitive variables**.

- **Model A Objective:** Minimize prediction error of environmental observations (images, joint positions, LiDAR).
    
- **Model B Objective:** Predict internal operational metrics, such as:
    
    - **Cumulative Epistemic Shock:** Predict its own multi-step future prediction errors (tracking when it _will_ get confused).
        
    - **Goal Persistence:** A contrastive loss that forces $z_{self}$ to remain invariant to environmental changes unless a high-level policy explicitly shifts the agent's intent.
        
    - **Action Consistency:** Predicting whether its physical actuators are executing actions exactly as commanded (detecting self-degradation or external resistance).
        

```
Model A (World Engine) ----> [Predicts External Sensory Data]
     |
  (Reads Context)
     v
[Stop-Gradient] 
     v
Model B (Self Engine)  ----> [Predicts Internal Meta-Metrics / Future Confidence]
```

### Mechanism III: Architectural Information Bottleneck

Give Model B a severe capacity bottleneck. If Model A has a latent dimension of 1024, give Model B a latent dimension of 32 or 64.

Because its capacity is so tiny, it cannot possibly store environmental maps or pixel data. It is forced to compress its representations into highly abstract, low-dimensional "macro-states" about the agent's internal condition—such as a scalar indicating confidence, a vector indicating active intent, or a topology map of its own blind spots.

## How to Formulate This Mathematically

If you were writing this up for a research paper, you could define the transition dynamics as:

$$\mathbf{z}_{world}^{t+1} \sim p_\theta(\mathbf{z}_{world}^{t+1} \mid \mathbf{z}_{world}^t, \mathbf{a}^t)$$

$$\mathbf{z}_{self}^{t+1} \sim p_\phi(\mathbf{z}_{self}^{t+1} \mid \mathbf{z}_{self}^t, \text{sg}[\mathbf{z}_{world}^t], \mathbf{a}^t)$$

Where $\text{sg}[\cdot]$ represents the **stop-gradient** operator. This mathematically ensures that Model B ($\phi$) adapts to the world ($\theta$), but the world model remains completely unconcerned with self-reflection, preserving a clean separation of roles.