- **World Model Sufficiency:** _What is the minimal information a learned world model must capture to enable effective planning?_ (E.g. do we need pixel-perfect prediction or just task-relevant state features?).

- **Latent State Optimality:** _Is there an optimal latent dimensionality or structure for a given control task?_ (E.g. too large a latent space may complicate planning, too small may drop essential details.)

- **Information Retention:** _What task-relevant information is consistently lost by standard encodings and needed later for control?_ (For example, autoencoder-based representations may discard small but crucial cues.)

- **Prediction Objective Validity:** _Is next-step prediction (in observation or latent space) the correct learning objective for all tasks?_ (It may focus on low-level detail rather than decision-critical factors.)

- **Latent Consistency:** _How can we ensure that latent representations remain consistent over long horizons and varied observations?_ (Current world models drift over time.)

- **Multi-Scale Latents:** _Should latent states exist at multiple time scales simultaneously, and if so, how to learn and use them?_