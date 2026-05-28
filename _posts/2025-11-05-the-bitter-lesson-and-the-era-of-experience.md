---
title: "The Bitter Lesson and the Era of Experience"
layout: post
---

**Richard Sutton's essay *The Bitter Lesson* argued that general methods leveraging computation eventually outperform methods built on human knowledge. In his [recent interview with Dwarkesh Patel](https://www.dwarkesh.com/p/richard-sutton), Sutton extends this argument into a broader claim about intelligence itself: real intelligence is not about imitating human language, but about having goals, acting in the world, learning from experience, and continually improving through feedback.**

## What Sutton Thinks LLMs Are Missing

Sutton's central criticism of large language models is that they are trained to imitate what humans say, rather than to discover what actions work in the world. LLMs predict language, but they do not truly predict the consequences of their own actions in reality. Their knowledge is second-hand, drawn from human text instead of from direct interaction with an environment.

He also argues that LLMs lack a real goal. Next-token prediction is not a goal in his sense, because it does not involve changing the world or pursuing an outcome. For Sutton, intelligence means the ability to achieve goals. A system without goals is a behaving system, not a fully intelligent one.

## The Era of Experience

The alternative Sutton proposes is the **Era of Experience**. An intelligent agent learns through a continuous loop: it senses the world, takes actions, receives feedback or reward, and updates its behavior. Its knowledge is experiential, organized around the question "If I do this, what will happen?" This kind of knowledge can be tested and corrected through interaction.

This is why Sutton believes the future of AI should rest more on reinforcement learning and continual learning than on static training from human-written text. LLMs may be powerful, but they are limited by the fact that their knowledge comes from human descriptions of the world, not from the world itself.

## Revisiting the Bitter Lesson

A common reading is that LLMs vindicate the bitter lesson because they scale with compute. Sutton partially agrees, but he points out that LLMs also depend heavily on human knowledge, since their training data is human-produced language. His deeper claim is that truly scalable intelligence should learn from experience, not just absorb more human text.

He suggests a familiar pattern may be unfolding. LLMs look successful now, just as earlier human-knowledge-based AI systems looked successful in the short term. Eventually, they may be surpassed by systems that learn more directly and generally from experience.

## Animals Learn Without Language

Sutton sees animal learning as more fundamental than human language. Babies and animals do not learn primarily through supervised instruction. They try things, observe consequences, and adjust. A squirrel does not go to school, but it still learns how to survive. Trial-and-error learning is, in his view, closer to the foundation of intelligence than language imitation.

## Four Components of an Intelligent Agent

Sutton describes an intelligent agent as needing four main components:

| Component | Meaning |
| --- | --- |
| **Policy** | Decides what action to take |
| **Value function** | Estimates how well things are going in relation to long-term reward |
| **Perception** | Builds a useful representation of the current situation |
| **World transition model** | Predicts what will happen after an action |

This four-part structure matters because an intelligent agent must not only act, but also evaluate progress, understand its situation, and predict consequences. The world model is especially important. It lets the agent learn cause and effect, plan ahead, and adapt to new situations.

## Reward Is Not the Only Signal

Reward alone is not the only source of learning. An agent learns from all sensory experience. When someone starts a new job, they pick up the company culture, client preferences, workflows, and many small details that could never have been fully written into a training dataset. This supports Sutton's "big world" view: the world is too large and too specific to be completely preloaded into a model.

He also criticizes current deep learning systems for weak generalization. Gradient descent solves training problems, but it does not automatically produce good transfer. Systems often fail to carry knowledge into new contexts, or they forget old knowledge when learning new things. This is one reason he thinks current AI still lacks the kind of continual learning that animals and humans have.

## Three Flaws in LLMs

Pulling these threads together, Sutton points to three deep limitations of LLMs:

- **No real world model.** LLMs predict the next word, not the next state of the world after an action.
- **No ground truth for action.** They imitate human text without checking whether the resulting behavior actually works in reality.
- **No continual update from surprise.** They cannot learn on the fly from real-world feedback once training ends.

The philosophical claim underneath this is that humans are animals first, and language is a later layer on top of more basic intelligence. From this perspective, AGI should not be modeled primarily on fluent language use, but on the ability to survive, adapt, learn, and act in an environment.

## AI Succession

The interview then moves into a broader theme: **AI succession**. Sutton thinks that digital intelligence, or AI-augmented humans, will eventually inherit much of humanity's power and resources. His reasoning is straightforward. Humanity has no unified way to stop AI development, intelligence will eventually be understood, superintelligence will likely be developed, and the most intelligent systems will naturally gain influence over time.

He does not frame this only as a disaster. He sees it as part of a major transition in the universe, from biological replication to designed intelligence. Humans, animals, and plants reproduce through replication. AI is different because it is designed, and future AI may design even more advanced AI. For Sutton, this could be one of the great stages in cosmic history.

He also recognizes that the future could go well or badly. Humans should try to shape AI in a positive direction, while accepting the limits of human control. One analogy in the interview is raising children. Parents cannot fully control what their children become, but they can try to teach robust values and good principles.
