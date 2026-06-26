
An assumption in MBRL -> One step next latent prediction is necessary for learning dynamics

here is an idea -> why don't given a string of action sequences sampled from trajectories, i.e. given an action sequence vector of some arbitrary T, let the dynamics model directly predict what's gonna happen in that timestep, no intermediary?

problem -> LLMs are explicitly trained to do step by step reasoning as their latent states cannot be "rushed"

alternative? -> i notice a link towards time abstracted predictions. a task/scenario specific version of my idea could be utilized. where the model selects for itself a coarse level of "T" to train by, plan and predict with.

example :