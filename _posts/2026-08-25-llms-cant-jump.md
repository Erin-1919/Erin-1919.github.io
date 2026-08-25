---
title: "LLMs Can't Jump: What Is a Researcher For When Research Is Automated?"
layout: post
mathjax: true
---

**[LLMs can't jump](https://www.tomzahavy.com/files/llms-cant-jump.pdf), a position paper by Tom Zahavy at Google DeepMind, argues that AI has become good at finding patterns in data and at deriving consequences from assumptions, while the step between the two, inventing the assumption, remains out of reach. The argument is about AI. The consequence I keep returning to is about researchers, and what we are for once the rest of the process runs itself.**

## The Paper in Short

Einstein sketched how discovery works in a letter to Maurice Solovine. You start from experience, you arrive somehow at axioms, and from those axioms you derive predictions you can test:

$$\text{experience } E \;\xrightarrow{\;\text{jump}\;}\; \text{axioms } A \;\longrightarrow\; \text{predictions } S$$

Going from axioms to predictions is mechanical. Getting to the axioms is the jump, the step the title puts beyond an LLM's reach.

Zahavy sorts reasoning into three kinds. **Induction** finds a rule from many examples, as most machine learning does. **Deduction** works out the consequences of a rule you already hold. **Abduction** invents an explanation that accounts for something surprising. AI is strong at the first, improving quickly at the second, and absent on the third.

General Relativity anchors the argument, and the choice of example is doing work. Of the major discoveries, it resists explanation in terms of data, error, and search more than any other.

### Why induction is insufficient

Induction learns patterns from many examples. Einstein lacked examples. Newton's theory already worked extremely well, and the observations agreed with it. Mercury's orbit was the one real anomaly, and the standard response was to postulate an undiscovered planet tugging on it. For a scientist modelled as an error-minimizer, the error was already near zero:

$$L_{\text{Newton}} \approx 0$$

An error-minimizer sitting at zero error has little reason to move, least of all toward curved four-dimensional spacetime. A system that prefers short explanations lands on the extra planet, since one more planet costs far less than rewriting what space, time, and gravity mean. Compression accounts of creativity, which equate discovery with finding shorter descriptions of data, leave this case unexplained.

### Why deduction is insufficient

Deduction tells you what follows from assumptions you already hold, and AI is improving fast here. Formal provers such as AlphaProof handle the move from axioms to consequences with increasing reliability. Hand a system the Equivalence Principle, that acceleration and gravity are locally the same thing, and it can work out much of what follows. Hand it the seven physical properties Einstein wanted his equations to satisfy, and the search for equations meeting them becomes a well-posed problem.

Deduction cannot originate the assumptions themselves. You cannot derive your axioms from those same axioms. The hard part is inventing the Equivalence Principle, and neither formal proving nor constrained search reaches that step.

### Why an LLM cannot make the jump

Einstein got there by imagining an experience. A person falling from a roof does not feel their own weight, and inside a closed accelerating box, acceleration and gravity produce identical local measurements. From that imagined situation he leapt to a principle, that the two cases are physically the same. Zahavy calls the move **manipulative abduction**, built from two operations, imagining an experience and then inventing an explanation for it.

An LLM stalls here because its symbols point only at other symbols. A language model learns relations among words produced from other words, so it learns that "gravity" sits near "falling" and near "mass". Einstein's move ran between symbol and sensation. He compared a remembered feeling of weight against an imagined feeling of acceleration and found them identical. Zahavy ties this to the symbol grounding problem and the Chinese Room. A model knows how people talk about gravity without inhabiting a world where gravity means anything, and on this account scale alone leaves the gap open.

### The proposed solution: world models

The prescription is a physically grounded, interactive model. The distinction Zahavy draws separates a video generator from a simulator. A video model predicts that an unsupported apple falls, because that continuation is statistically common. Statistical continuation and causal structure are different things, and only the second supports intervention.

An interactive world model accepts interventions. Remove the support. Double the acceleration. Cut the elevator cable. Switch gravity off. This is Pearl's territory, where counterfactuals replace correlations, and systems like Genie point in the direction. The target loop looks like this:

$$\text{world model} \rightarrow \text{counterfactual experiment} \rightarrow \text{observation} \rightarrow \text{hypothesis} \rightarrow \text{axiom} \rightarrow \text{deduction} \rightarrow \text{verification}$$

### The distinction that matters

Zahavy grants that AI discovers a great deal, and he separates two kinds of discovery. **Discovery within a framework** supplies the rules, the goal, and a scoring function, and leaves search as the work. AI is already very good at this. **Discovery of the framework** requires inventing the concepts and assumptions before anything can be scored. The gap sits in the second.

## What This Means for Researchers

Google's AI co-scientist, DeepMind's AlphaEvolve, and the various AI Scientist pipelines all appeared within about a year of each other, and they made me ask to ask: what a researcher is actually for. Most of the skills I spent years building now have an automated version. A system can read more papers than I can, write cleaner code, run far more experiments, and put together a draft in an afternoon.

The paper helped me see that all of that sits at the back end of the process. Reading, coding, running experiments, analyzing results, and writing up are the later stages. Before any of them, someone decided what question to ask, which variables matter, and how to set the problem up. That first decision is the part nothing automates yet, and it is also the part that decides how much the rest of the work is worth.

Einstein is a good illustration. Grossmann was the stronger mathematician of the two, and Einstein relied on him for the geometry. Einstein's contribution was the question of what happens if acceleration and gravity are the same thing. Once that question was on the table, the rest of the work had somewhere to go.

This changes how I think about my own value. Being able to run a research process well matters less than it used to, because that part is being automated. Being able to decide what is worth working on, and how to frame it, matters more. The hardest version of that skill is noticing that a whole field is solving the wrong problem.

It also gives a stronger meaning to human in the loop. Usually that phrase means the AI does the work and a person checks it. The more useful version is a person who stays outside the loop and asks whether the loop is the right one. A system can optimize a loss function very well without anyone asking why that loss function, whether those variables are the right ones, or whether the quantity being measured is the one we actually care about. Those questions sit above the optimization, and they are the ones I want to spend my time on.

---

***Automated research is very good at searching a space. The researcher's job is deciding which space is worth searching, and occasionally inventing a new one.***
