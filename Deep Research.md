- **World Model Sufficiency:** _What is the minimal information a learned world model must capture to enable effective planning?_ (E.g. do we need pixel-perfect prediction or just task-relevant state features?).

- **Latent State Optimality:** _Is there an optimal latent dimensionality or structure for a given control task?_ (E.g. too large a latent space may complicate planning, too small may drop essential details.)

- **Prediction Objective Validity:** _Is next-step prediction (in observation or latent space) the correct learning objective for all tasks?_ (It may focus on low-level detail rather than decision-critical factors.)

- **Multi-Scale Latents:** _Should latent states exist at multiple time scales simultaneously, and if so, how to learn and use them?_

- **Memory Integration:** _What is the role of memory in extended decision-making?_ (What should memories store, and how should planners query memory vs sensory inputs?)

- **Exploration Utility:** _What truly makes an experience “useful” for an agent, beyond simple novelty?_ (E.g. tasks where novelty-based signals lead to dead ends.)

- **Learning vs Planning Loop:** _What information should the planner query from the world model (e.g. reward vs transition vs latent dynamics) for optimal planning?_


