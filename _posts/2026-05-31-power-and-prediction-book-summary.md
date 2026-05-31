---
title: "Book Summary: Power and Prediction by Agrawal, Gans, and Goldfarb"
layout: post
---

![book](/assets/img/20260531/book.jpg)

**This post contains my chapter-by-chapter summary of *Power and Prediction: The Disruptive Economics of Artificial Intelligence* by Ajay Agrawal, Joshua Gans, and Avi Goldfarb. This is the sequel to *Prediction Machines*, and it shifts the focus from the economics of cheap prediction to the disruption that follows when AI moves from point solutions to full system redesign.**

**Listen to a NotebookLM-generated podcast on this content:** [Listen here](https://drive.google.com/file/d/1kl845DHikdx7SzW7cILY73YF7ZLz7YFc/view?usp=sharing)

## Part One: The Between Times

### 1. A Parable of Three Entrepreneurs

- The parable of the three entrepreneurs, set over a hundred years ago in the market for energy, illustrates how different approaches to the same technology shift, from steam to electricity, can lead to very different value propositions. Point solutions focus on reducing power costs and friction without altering factory designs. Application solutions involve modular machines that operate independently. System solutions involve redesigning factories for optimized workflows and spatial layouts.

- Some value propositions are more attractive than others. Initially, point and application solutions that simply replaced steam with electricity without system changes offered limited benefits, which was reflected in slow industry adoption. Entrepreneurs who implemented system-level solutions by decoupling machines from their power sources realized significantly greater value, because these designs were impossible or too expensive with steam.

- Just as electricity decoupled the machine from the power source and shifted the value proposition from "lower fuel costs" to "vastly more productive factory design," AI decouples prediction from the other aspects of a decision. This shifts the value proposition from "lower cost of prediction" to "vastly more productive systems."

### 2. AI's System Future

- Despite the predictive power of AI, measured productivity growth has declined by half over the past decade, and real income has stagnated since the late 1990s for most Americans. This productivity paradox is not new. A similar pattern appeared in the 1980s with computers. The authors call this period The Between Times: after witnessing the power of AI and before its widespread adoption. Point and application solutions can be implemented quickly, but the system solutions that unlock AI's full potential take much longer.

- The key concept distinguishing the three types of AI solutions is independence. If an AI prediction creates value by enhancing a focal decision, and that value is independent of any other changes to the system, then a point solution or an application solution is feasible. If the value of the enhanced decision instead requires other substantive changes to the system, then a system solution is required.

- System solutions are harder to implement than point or application solutions because the AI-enhanced decision impacts other decisions in the system. Point and application solutions tend to reinforce existing systems, while system solutions upend them and therefore often result in disruption. System solutions are likely to generate the greatest overall return on AI investment, and they create winners and losers across industries.

### 3. AI Is Prediction Technology

- Recent advances in AI have caused a drop in the cost of prediction. Prediction takes information we have and generates information we need but do not have, such as whether a current financial transaction is fraudulent. When the cost of an input falls, we use more of it, so cheaper prediction means more AI. As prediction becomes cheaper, the value of substitutes such as human prediction falls, while the value of complements rises. The two main complements are data and judgment. Prediction is an expression of likelihood, and judgment is an expression of desire, so every decision combines the likelihood of each outcome with how much we value it.

- Perhaps the greatest misuse of AI predictions is treating the correlations they identify as causal. Correlations are often good enough for an application, but when a causal relationship is needed, randomized experiments remain the best tool for discovering what causes what.

- *Prediction Machines* introduced a thought experiment about Amazon's recommendation engine becoming so accurate that Amazon could ship products before customers order them. Although Amazon filed a patent for "anticipatory shipping," it has not adopted the model. The original point solution leverages Amazon's existing system, but the new model would require redesigning the system, especially how returns are handled. The threshold in the thought experiment required shifting from a point solution to a system solution, a difference the earlier book underappreciated.

## Part Two: Rules

### 4. To Decide or Not to Decide

- Rules are decisions made preemptively. Making a decision, unlike following a rule, allows us to account for information available at the time and place of the decision, so actions from decisions are often better than actions from rules. Decisions carry a higher cognitive cost, which is worth paying when the consequences are significant and the cost of information is small. AI does not change the consequences, but it lowers the cost of information.

- The trade-off between rules and decision-making is central to AI because the primary benefit of AI is to enhance decision-making. AIs provide little value for rules. By lowering the cost of prediction, AI raises the relative returns to decision-making, so advances in AI will liberate some decision-making from rule-following.

- Rules incur lower cognitive costs and also enable higher reliability. One decision often affects others, so in systems with interdependent decisions, reliability matters. Standard operating procedures are rules that reduce cognitive load and enhance reliability. Using AI prediction to turn rules into decisions may require redesigning the system to account for the reduced reliability.

### 5. Hidden Uncertainty

- The target of opportunity for AI-enabled decisions is not just the rules themselves but the edifices and scaffolding built up to hide the uncertainty that makes those rules wasteful and inefficient.

- Modern airports are an example of expensive scaffolding constructed to hide uncertainty. The main sources of uncertainty are delays from traffic and security. Lavish airport designs help passengers forget that they are operating under a rule forcing them to arrive long before departure.

- In greenhouses, AI predictions of pest infestations can help growers prevent them, which is a point solution. If pest prediction becomes good enough, AI could enable system-level change instead. Because the structural design and workflow of a greenhouse are shaped by the risk of infestation, better prediction would let farmers grow more pest-sensitive crops, operate larger greenhouses, and pursue new energy-saving strategies.

### 6. Rules Are Glue

- Like standard operating procedures, checklists are a manifestation of rules and the need to follow them. They ensure reliability and reduce error. Switching from a rule to a decision may improve a particular action, but it can create uncertainty and problems for other people in the system.

- Rules glue together in a system, which is why it is hard to replace a single rule with an AI-enabled decision. A very powerful AI often adds only marginal value because it is dropped into a system whose many parts were designed to accommodate the rule and resist change. The parts are interdependent, glued together.

- A personalized education AI that predicts the next best content for a learner would be stifled if dropped into a system built around the age-based curriculum rule. Embedding the same AI into a new system that leverages personalized discussion, group projects, and teacher support would likely have a much bigger impact. The primary challenge is not building the prediction model but unsticking education from the age-based curriculum rule that glues the system together.

## Part Three: Systems

### 7. Glued versus Oiled Systems

- Social distancing was a rule used to manage the pandemic, and it was expensive. It shut down large parts of the education system, the health-care system, and the world economy, with mental health impacts that will take decades to understand. Many other rules were built around it, including restaurant capacity limits, transit protocols, school teaching methods, and emergency care procedures.

- While most people viewed Covid-19 as a health problem, the authors reframe it as an information problem. For the infected, it was a health problem, but for the uninfected majority it was an information problem, because without knowing who was infected we had to treat everyone as potentially infected. Accurate prediction could have solved the information problem by quarantining only those likely to be infectious. Rules are the primary target when looking for new decisions that AI prediction can unlock.

- Turning rules into decisions requires a system that can accommodate the change. If one rule is glued to another for the sake of reliability, inserting a decision may be fruitless. The authors describe an oiled system of twelve large companies whose CEOs directed leadership teams to make information-based decisions using rapid antigen testing to predict employee infectiousness. This kept the businesses running where the prevailing system would have forced a shutdown, and the demonstrated success led over 2,000 more organizations to adopt it.

### 8. The System Mindset

- Task-level thinking is the dominant approach to planning AI adoption. It identifies specific tasks in an occupation that AI can perform more accurately, faster, or more cheaply than a human. Corporate leaders, management consultants, and academics have largely converged on this approach.

- The dominance of task-level thinking is surprising, because the most dramatic AI implementations to date are not task-level replacements of human labor but new system-level designs that prediction makes possible, as at Amazon, Google, Netflix, Meta, and Apple. Task-level thinking leads to point solutions motivated by cost savings through labor replacement. System-level thinking leads to system solutions motivated by value creation.

- Health care has many potential AI applications, including disease diagnosis, automated surgery, at-home monitoring, personalized treatments, and drug discovery, yet it has seen only marginal benefit so far. Some of this is due to regulatory approval timelines, but much is due to the muted benefits of point solutions inside the existing system. A system solutions approach requires starting from a blank slate and rethinking training, delivery, compensation, privacy, and liability. That is the system mindset.

### 9. The Greatest System of All

- Innovations in the innovation system itself can cascade downstream onto many other systems. Advances in lens-grinding technology improved personal optics such as eyeglasses and also research tools such as microscopes. The microscope led to the germ theory of disease, which made battling viruses and bacteria feasible and transformed medicine.

- One core role for AI in the innovation system is predicting the consequence of new combinations. Where we previously relied on scientific theory or trial and error, AI prediction can now generate hypotheses when sufficient data exists to train the models.

- Automated hypothesis generation may significantly enhance innovation productivity, but capturing the benefit requires rethinking the entire innovation system rather than the single step of hypothesis generation. Faster hypothesis generation has little impact if hypothesis testing remains unchanged and simply becomes a downstream bottleneck.

## Part Four: Power

### 10. Disruption and Power

- Incumbents can often adopt point solutions easily because they improve a specific task without requiring changes to related tasks. They struggle with system-level solutions, which demand changes to tasks the organization has already optimized and which may be inferior on some tasks in the short run. That sets the stage for disruption.

- Power here means economic power. You have power if what you own or control is scarce relative to demand. Scarcity can be reduced by competition, which is why economists sometimes treat economic power and monopoly power as equivalent. When something previously scarce is exposed to competition, power shifts.

- Because fully benefiting from AI often requires a system-level solution, the redesign can shift power at the industry level, where data-rich industries become more powerful, at the company level, and at the job level, as when Blockbuster franchises lost power in the shift to online and mail-delivery movie rentals. Those who stand to lose power resist change, and because they currently hold power they may be effective at preventing system-level change. That creates the context for disruption.

### 11. Do Machines Have Power?

- Machines cannot make decisions, but AI can fool people into thinking they do. Machines appear to decide when we codify judgment. The AI generates a prediction, and the machine then draws on codified human judgment to execute an action.

- AI predictions are imperfect, so we mitigate the risk of being wrong in two ways. Before deployment, we work through contingencies and decide what action the machine should take in each one. After deployment, we keep a human in the loop to step in when the AI cannot predict with high enough confidence or encounters a scenario for which judgment has not been codified.

- Although machines do not have power, they can create power through scale and reallocate power by shifting whose judgment is used where and when. AI systems can decouple judgment from the decision so it can be provided at a different time and place. When judgment shifts from being applied individually to being codified into software, this can scale and shift market share, and it can change who makes the decision, moving power to whoever provides the judgment for codification or owns the system in which it is embedded.

### 12. Accumulating Power

- Despite the challenges of system-level innovation, there is good reason to start sooner rather than later, because AI confers an advantage on first movers. AI learns, so the sooner it is deployed, the sooner it improves, and the better its predictions, the more effective the new system becomes.

- Because AI is software, the marginal cost of one more prediction is close to zero. If one AI becomes slightly better early in a market, more users move to it, generating more feedback data, which produces better predictions and attracts still more users. Once this flywheel spins, a small early advantage can grow into a large one. The prize for being first is so large that companies invest more aggressively than seems rational, which leads to racing.

- Feedback loops have significant implications for system design, because an AI can only learn if it has access to outcome data. An educational AI that predicts the next best content for a learner must be designed to collect feedback as frequently as possible, both to confirm learning and to assess engagement. This is not a point solution dropped into the existing system but a redesign that collects high-frequency feedback data measured in minutes rather than midterms.

## Part Five: How AI Disrupts

### 13. A Great Decoupling

- Prediction and judgment are the two primary ingredients of decision-making. In a decision tree, prediction generates the probability of each branch, and judgment generates the payoffs at the ends of each branch. Usually we do not notice that prediction and judgment are separate inputs, because both sit in the mind of the same decision-maker. Introducing AI shifts the prediction from a person to a machine, decoupling it from judgment, which may change who provides the judgment.

- We make decisions constantly without consciously separating prediction from judgment, yet judgment can be inferred after a decision through analytical techniques, what economists call "revealed preference." Economists and marketers have long used statistical tools to measure judgment from observed choices.

- Decisions are the primary building blocks of a system. Before AI, the distinction between prediction and judgment was irrelevant to system design because both happened in one mind. AI changes that. When prediction moves to a machine, we can rethink the system: predict more often, predict for less important decisions, codify judgment to automate and scale the decision, or assign the judgment role to people with better judgment. The opportunity is large because AI creates new options at the most fundamental level, decision composition.

### 14. Thinking Probabilistically

- AIs introduce probabilistic thinking into a system. When we investigate a car accident, we ask whether the driver saw the pedestrian and expect a yes or no answer. An AI instead reports that it saw something it thought was a human with, say, a 0.01 percent likelihood. Introducing an AI often transforms a system from deterministic to probabilistic. Sometimes the existing system accommodates a probabilistic input well, and other times this creates an opportunity for greatly enhanced productivity through redesign.

- Translating a prediction into a decision requires judgment. If people traditionally made the decision, the judgment may not be codified separately from the prediction, so it must be generated, either through transfer by learning from others or through experience. Without existing judgment we have less incentive to build the prediction AI, and without the AI we hesitate to develop the judgment, creating a chicken-and-egg problem that complicates system redesign.

- Fully exploiting AI will often require system-level solutions that include not only prediction and judgment but also a regulatory function to reassure society as systems move from deterministic to probabilistic. Because the system is not hard-coded, we cannot know in advance how it will behave in every scenario. Much as the pharmaceutical industry benefited from a regulatory process that assured citizens the benefits outweighed the risks, we may need an FDA-type function that tests machine decisions against an established framework.

### 15. The New Judges

- When implementing an AI decouples prediction from judgment, there is an opportunity to increase value creation, but it may require redesigning the system to move the locus of judgment from current decision-makers to others. When that happens, power is reallocated, because those who provide judgment ultimately decide. New designs may reduce the power of certain individuals, who may resist.

- In designing a new system, decision rights should go to the person or group most likely to decide in the organization's best interest at the lowest cost, which is decision efficiency. Four factors matter: information, skills, incentives, and coordination. The answers can differ greatly when the requirement is prediction plus judgment versus judgment only, because the AI now delivers the prediction.

- New system design may concentrate power when judgment is codifiable and therefore scalable. In credit card networks, power concentrated in a few companies rather than across many merchants. In radiology, AI's strength in pattern recognition and anomaly detection may centralize the prediction task, raising the question of whether radiologists are best suited to provide judgment, or whether nurses, social workers, or other professionals should.

## Part Six: Envisaging New Systems

### 16. Designing Reliable Systems

- Decisions do not operate in a vacuum. Often many other decisions or actions depend on the outcome of a single decision, which is why we sometimes use predetermined rules instead of real-time decisions. Rules enhance reliability, so we accept worse localized decisions in exchange for greater reliability across the system. Reliability is a key feature of systems with interdependent decisions.

- Two main approaches address the reduced reliability that AI-based decision-making introduces: coordination and modularity. Coordination specifies the overall objective and then designs information flows, incentives, and decision rights so each decision-maker optimizes for the overall goal. Modularity builds a wall around an AI-enhanced decision to avoid misalignment with other decisions, which reduces coordination costs but sacrifices synergies.

- Systems are combinations of interacting decisions, and they grow complex quickly. Three binary decisions produce eight combinations, ten produce 1,024, and twenty produce over a million. This complexity is why simulation is so powerful for system design. Digital twins can simulate different combinations, and AI can predict the outcome of each.

### 17. The Blank Slate

- Most companies have built systems of so many interdependent rules and so much scaffolding to manage uncertainty that it is hard to see how to undo parts of them. Rather than reasoning through how changing one rule ripples through the system, the authors suggest starting from scratch with a blank slate. The AI Systems Discovery Canvas has three steps: articulate the mission, reduce the business to the fewest decisions needed to achieve the mission if you had super-powerful AIs, and specify the prediction and judgment associated with each primary decision.

- Home insurance can be reduced to three primary decisions: marketing, which allocates resources for customer acquisition; underwriting, which sets premiums or declines coverage; and claims, which decides whether a claim is legitimate and pays it. With three high-fidelity AIs predicting the lifetime value of a client times the probability of conversion, the likelihood of a claim times its magnitude, and the legitimacy of claims, a firm could redesign a fast, efficient, low-cost, and highly profitable business that beats competitors on price and convenience, which is exactly the goal of new insurtech firms.

- The canvas also reveals new business opportunities. If an AI predicting claim likelihood and magnitude becomes good enough to work at the peril or sub-peril level, such as a sensor detecting heightened electrical fire or flooding risk, the insurer could identify which risk mitigation solutions are worth their cost, subsidize the device, and lower the premium. This offers customers a new value proposition: the insurer not only transfers risk but reduces it. Fully exploiting this requires a system designed to be optimized for risk mitigation.

### 18. Anticipating System Change

- Two economists built an AI that was superhuman at predicting heart attacks, cheaper, faster, and less error-prone than the average doctor on both false positives and false negatives. As a point solution, it would impact a single decision, whether to administer a test, improving the hospital's productivity by allocating heart attack detection tests better.

- The same highly accurate AI could underpin a system-level solution with far greater impact. Using the AI Systems Discovery Canvas, a key decision is whether to test, based on the prediction of a heart attack. If that prediction becomes good enough with easily collected data, such as from a smartwatch, those predictions could move out of the hospital's emergency triage and into the patient's home, so many patients would never need the hospital and could be treated by a pharmacist or primary care physician.

- A key attribute of the canvas is that it abstracts the organization to its core decisions, separating the fixed mission from the dispensable rules and decisions of the status quo. Designers are then free to imagine many system-level solutions enabled by powerful prediction. A single heart attack prediction AI could underpin several alternatives. The process begins by identifying the key decisions, speculating on what becomes possible if predictions are highly accurate, and reimagining the systems that exploit those predictions for mission success.

## Epilogue: AI Bias and Systems

- The popular narrative is that AIs learn human bias and amplify it. The authors agree and advocate constant vigilance. When AI is implemented as a point solution, it can amplify existing biases and increase discrimination, which produces the negative headlines we see and can create appropriate resistance to adoption.

- A common argument holds that AI should not be used in important decisions like hiring, bank loans, insurance claims, legal rulings, and university admissions because the models are opaque black boxes that perpetuate discrimination. The authors disagree. They argue AI should be used in these decisions precisely because it is scrutable in a way humans are not. We cannot interrogate a human hiring manager with thousands of counterfactual questions like "Would you have hired this person if they were exactly the same, except white?" and expect an honest answer, but we can ask exactly that question, and thousands more, of an AI system and get rapid, accurate answers.

- Viewed through a system mindset, AIs can be designed to reduce discrimination, and they can be monitored continuously and retroactively to ensure success. Those who benefit from existing biases will resist, but there is reason for optimism. University of Chicago professor Sendhil Mullainathan contrasted his studies of human discrimination in hiring and AI discrimination in health care and noted how much easier it is to detect and fix discrimination in algorithms than in people, since software can be updated while human "wetware" cannot. Both humans and AIs will be biased, but AI bias can be detected and addressed.

---

***Where *Prediction Machines* explained why cheap prediction reshapes decisions, *Power and Prediction* argues the real payoff comes from redesigning entire systems around it, and that the slow, contested work of system change is what The Between Times is really about.***
