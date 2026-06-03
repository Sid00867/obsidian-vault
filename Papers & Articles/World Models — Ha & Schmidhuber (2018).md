![[Pasted image 20260603225847.png]]

![[Pasted image 20260603225923.png]]

![[Pasted image 20260603230048.png]]

In our approach, we approximate p(z) as a mixture of Gaussian distribution, and train the RNN to output the probability distribution of the next latent vector z t+1 given the current and past information made available to it

![[Pasted image 20260603234743.png|626]]![[Pasted image 20260603234819.png]]
![[Pasted image 20260603234849.png]] ![[Pasted image 20260604000525.png]]

Furthermore, we see that in making these fast reflexive driving decisions during a car race, the agent does not need to plan ahead and roll out hypothetical scenarios of the future. Since ht contain information about the probability distribution of the future, the controller can just query the RNN instinctively to guide its action decisions.

We dont do planning nor imaginative training here. simply letting the controller have access to the model improves it