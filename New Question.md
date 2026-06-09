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