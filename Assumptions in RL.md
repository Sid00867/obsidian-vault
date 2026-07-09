
-> Pixel perfect predictions (fixed by JEPA)
-> one timestep predictions (fixed by slow moving latent/ hierarchical models)
-> fixed actions or skills (questioned and alternates proposed by macro actions, unsupervised skill learners, latent actions)
-> experience replay is used only during training (retrieval RL fixes this)
-> that reflexive policy network can practically model every scenario, and that a model only need an aid in training or planning (they can, but only in theory)
-> imaginative planning is actually useful instead of providing marginal coverage improvement over state-action space. (a true imaginative planner should be able to generate completely new scenarios it thinks it might falter in)
-> that the policy and the model are seperate, the model does pass its hidden state to the policy network, but there is no feedback from the policy to the model, only happens indirectly via the environment 