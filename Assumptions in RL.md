
-> Pixel perfect predictions (fixed by JEPA)
-> one timestep predictions (fixed by slow moving latent/ hierarchical models)
-> fixed actions or skills (questioned and alternates proposed by macro actions, unsupervised skill learners, latent actions)
-> experience replay is used only during training (retrieval RL fixes this)
-> that reflexive policy network can practically model every scenario, and that a model only need an aid in training or planning (they can, but only in theory)
-> imaginative planning is actually useful instead of providing marginal coverage improvement over state-action space. (a true imaginative planner should be able to generate completely new scenarios it thinks it might falter in)
-> that the policy and the model are separate, the model does pass its hidden state to the policy network, but there is no feedback from the policy to the model, only happens indirectly via the environment.
-> metareasoning is nonexistent. a few vague sense of predictors akin to it exist, like confidence/entropy/trust value etc. but none actually explictly plan over planning/imagining/reacting (but tbf this topic is not really definable in the context of MBRL)
-> we trust the model will remember and forget details for planning in its latent state automatically, but we have no explicit/empirical proof for this, even if we do, they dont seem to be working for long horizon tasks.


# Pain points

it feels like there should be a way to accelerate the "helplessness" phase of RL training.
perhaps some useful prior or learning paradigm.

foundational models have a useful prior for a lot of tasks.

during early exploration, instead of sampling actions randomly every timestep, we sample a sequence size of N of the same action. when the state stops changing meaningfully or when a sequence has ended, we sample a different action sequence vector. we stop this method when out agent has gained some competency.

here is another idea -> a seperate policy, for exploration. its goal : reaching novel states. it could be even be task/env agnostic by first training on an env to predict not actions but some vague sense of "action structure" based upon environment feedback, and use that to generalize other explorative phases in other environemnts
