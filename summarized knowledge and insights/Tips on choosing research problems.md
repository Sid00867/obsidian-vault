
[Attributes of a great research question - by Paras Chopra](https://letters.lossfunk.com/p/attributes-of-a-great-research-question)
 A good research question
 -> surprising to expert
 -> fruitful and consequential
 -> feasible

https://drive.google.com/file/d/1320N9ZHnA_MMoyUy8pR9yNdUq0MRZEBd/view?usp=sharing
Exploration Sprint template

## Common pitfalls in AI research
Not reading everything you can on a given domain. You should only stop reading (relevant) papers in your domain when your net new knowledge starts approaching zero in that domain.

Also, when you read, read actively. Make notes. Summarise key ideas. Write what they missed out and what can you improve upon.

Paras chopra notes - [Catching up on Model Based Reinforcement Learning - Google Docs](https://docs.google.com/document/d/1JYNnyfLVHMp7JACr4G6qAtxIiCSmoKYxuoUXxTwjOIo/edit?tab=t.0)


![[Pasted image 20260603132939.png]]

#### Confusing building things with doing science

In AI research, many people come from an engineering background. As an engineer, your primary job is to build stuff that works in the real world. And that’s hugely valuable as our economy runs on useful things we have in our life.

But, a scientist’s mindset is different.

**A scientist’s job is to make precise claims about a phenomena and then provide evidence for such claims**

a lot of uncertainties are mostly personal uncertainties - where someone somewhere out there knows the answer, but you don't. In that case, **finding out whether the uncertainty you have is an actual uncertainty in a community or it's a personal uncertainty is a good first step**.

Doing a literature review and background survey is essential


![[Pasted image 20260603133839.png|697]]
![[Pasted image 20260603134133.png]]

![[Pasted image 20260603134110.png]]![[Pasted image 20260603143205.png]]This tree is a living process. **Before you jump to selecting a research question from this tree, it might be important for you to read the literature widely and refine your understanding**.

Once you have a decomposition of your question / problem of interest that you’re satisfied with, you need to start filling the nodes.

What to fill in each node:

> **Write foundational assumptions and key results in each node, and what uncertainties still unresolved.**

Once you have nodes filled in, rank uncertainties by impact, neglectedness, and tractability to shortlist questions/uncertainties you want to focus on during the next 6-9 months.

### Examples of the four levels of research uncertainties

#### Level 1 - Known uncertainties

- How to achieve sample-efficient RL?
    
- How to make LLMs more interpretable?
    
- How to prevent catastrophic forgetting in continual learning?
    

#### Level 2 - Foundation assumptions

- Is the scaling hypothesis correct? Under what circumstances does it fail? (This questions the basic assumption that "bigger models = better models")
    
- Can we formulate a different objective function for language models other than auto-regressor next to completion? (This questions the dominant current pardigm of training models)
    
- Should we optimize for reward maximization at all? (This questions the basic assumption of RL.)
    

#### Level 3 - Conceptual blind spots

- Relationship between consciousness and intelligence. (Current ML theory is completely mechanistic)
    
- Non-computational forms of intelligence. (We lack vocabulary for it)
    
- Collective intelligence. What does the word 'collective' here even mean?
    

> **As you can see, the higher the level you go, the more impactful your research is going to be,** but the less feasible that research could be because the uncertainty is going to just balloon up.


![[Pasted image 20260603143834.png]]- **Don’t propose solutions** until the problem has been discussed as thoroughly as possible.
