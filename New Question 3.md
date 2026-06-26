
An assumption in MBRL -> One step next latent prediction is necessary for learning dynamics

> here is an idea -> why don't given a string of action sequences sampled from trajectories, i.e. given an action sequence vector of some arbitrary T, let the dynamics model directly predict what's gonna happen in that timestep, no intermediary?

problem -> LLMs are explicitly trained to do step by step reasoning as their latent states cannot be "rushed"

alternative? -> i notice a link towards time abstracted predictions. a task/scenario specific version of my idea could be utilized. where the model selects for itself a coarse level of "T" to train by, plan and predict with.

example : in atari pong, the agent does not need to predict every frame of the game to make accurate predictions

problem -> how do you bundle action sequences towards the latent state training objective? what happens in planning?

> an idea -> COARSE action variables. i just realized there could be a level of abstraction in the action space too that could be learnt during training and utilized when available and necessary.
> like "go there" instead of "take a step using you left foot"

isnt this just subgoal generation? how is it any different?

https://chatgpt.com/share/6a3ec49b-1bb8-83ee-883b-297628e77053

![[Pasted image 20260627000132.png]]

this would make planning cheap, if possible

![[Pasted image 20260627000234.png]]


CHECKOUT  "LATENT ACTIONS"