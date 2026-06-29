Basic idea:

Two networks exist -> IDM and FDM (Inverse/forward dynamics model)

given an unlabeled action dataset of some observation transitions, IDM learns to predict a highly compressed representation of a transitions in an action space, as a latent action variable Z.
(basically predict the action between two transitions)

How do we incentivize the IDM to learn an "action"?

we build a FDM that takes the latent action predicted by the IDM, and use the same transition tuple the IDM was trained on, but this time only the previous observation and latent action is used to predict the future observation

this ensures that we capture some notion of a "action that results in a specific transition", given that we ensure that the IDM passes a highly compressed representation to the FDM, ensuring the IDM doesnt cheat by passing in the entire future obs to the FDM.

![[Pasted image 20260629135544.png|275]]


we then learn a encoder that maps the latent action to the real action space, and even train a latent policy.


