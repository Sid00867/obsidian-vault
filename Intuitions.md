
-> If you want a genuinely open angle here: most world-model work treats the encoder as fixed-capacity and lets gradient descent decide what survives compression implicitly. Explicitly parameterizing "what gets forgotten" as an action with its own objective (rather than an emergent byproduct of a bottleneck) is less explored.

-> a teacher-student pair where the teacher isn't trying to be correct, it's trying to be _persuasive_, and the student's job is calibration — learning to discount confident-sounding but wrong arguments.

-> That asymmetry suggests reasoning's evolutionary function was persuasion and justification within a group, with truth-tracking as a secondary, sometimes incidental, byproduct. **Why it might be true:** Mercier and Sperber's "argumentative theory of reasoning" explains confirmation bias (a notorious "flaw") as functional: if reasoning's job is to construct the strongest case for a position you already hold, seeking confirming evidence is exactly correct behavior, not a bug. its why groups reasoning together often produce _better_ answers
		-> a sort of training paradigm where a teacher model "competes" with the student model in some vague "argumentative" sense?

-> Loewenstein's "information gap theory" predicts (and finds) that curiosity intensifies right around the point where you know _just enough_ to realize what you're missing
				-> if this hasnt been done before, find a way to quantify this

-> People get stuck on problems not from lack of raw ability but because an object or concept's most recent or most typical use "locks" its representation, blocking recognition of other equally valid uses — and this locking effect is strongest exactly when the fixating use was made most salient or recent.
		-> are there scenarios in MBRL where our representations gets "stuck" in a minima. (i have no idea what that could mean in MBRL)?

-> There's a specific band of task difficulty — too hard to do alone, but doable with help — where learning is maximized; below it there's nothing to learn, above it the learner can't productively engage even with assistance. (doesnt curriculum learning just solve this?). Vygotsky's "zone of proximal development"
		-> same as information gap theory, if it hasnt been done before, is there a way to quanitfy it?
