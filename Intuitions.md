
-> If you want a genuinely open angle here: most world-model work treats the encoder as fixed-capacity and lets gradient descent decide what survives compression implicitly. Explicitly parameterizing "what gets forgotten" as an action with its own objective (rather than an emergent byproduct of a bottleneck) is less explored.
			-> can we train a deep network that basically transforms a latent state (preserving its dimensions) under some optimization objective to "forget this or reinfrocing remeber that"? are there any such "transformations" to latent state we can do with new and novel training objectives? not just memory?

-> a teacher-student pair where the teacher isn't trying to be correct, it's trying to be _persuasive_, and the student's job is calibration — learning to discount confident-sounding but wrong arguments.
			->a UED or currciulum design paradigm that identifies/constructs environments where an agent gets the sort of "persuasive" pressure to attempt something??


