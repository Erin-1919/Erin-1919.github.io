---
title: "Notes from Introduction to Generative AI (Spring 2024)"
layout: post
---

**This post contains my personal notes from the course *Introduction to Generative AI* (Spring 2024), taught by Prof. Hung-yi Lee at National Taiwan University. The course provides a comprehensive overview of generative models.**  

Course link: [https://speech.ee.ntu.edu.tw/~hylee/genai/2024-spring.php](https://speech.ee.ntu.edu.tw/~hylee/genai/2024-spring.php)

## Course Notes

### Overview of Generative AI

- Generative AI refers to models that can produce complex and coherent content such as text, images, audio, or video, often based on patterns learned from large datasets.

- A large language model (LLM) generates text by predicting the next token based on the context. This context can come from the model's pre-trained knowledge, the current prompt, and any additional input provided at runtime (such as retrieved documents or API outputs).

- LLMs generate text by predicting the next token based on available context. This context includes the model’s pre-trained knowledge, the prompt provided by the user, and additional information retrieved at runtime through methods like Retrieval-Augmented Generation (RAG).

- LLMs use the transformer architecture to predict the next token. At each step, the model outputs a probability distribution over all possible tokens, then selects one — either the most likely or by sampling, similar to rolling a weighted dice.

### Prompting and Inference Strategies

- There are two general ways to improve the outputs of large language models. First, at inference time, we can use prompt engineering, external tools (like search or calculators), or multi-agent collaboration. These approaches don’t require modifying the model itself. Second, we can improve the model’s behavior by changing how it is trained — through stages like pre-training, instruction tuning, supervised fine-tuning, and reinforcement learning from human feedback (RLHF).

- Prompt engineering is the practice of crafting prompts to help language models produce better responses without retraining the model. Techniques include encouraging step-by-step thinking, assigning roles, or prompting self-reflection. These strategies were especially impactful for earlier models, but even with modern powerful LLMs, good prompting remains important—especially in complex, multi-step, or specialized tasks.

- There are many advanced prompt engineering strategies designed to guide LLM reasoning, often named in the 'X of Thought' format. These include Chain of Thought, Tree of Thought, Algorithm of Thought, and Program of Thought. Each of these aims to structure how the model approaches a problem — whether step-by-step, through branching logic, algorithmic reasoning, or code generation.


### Training and Alignment

- There are generally three stages of LLM training: pre-training, instruction fine tuning, and reinforcement learning from human feedback (RLHF).

- The result of pre-training is called a foundation model — a large, general-purpose language model with broad knowledge but no task-specific behavior. Instruction tuning and reinforcement learning from human feedback (RLHF) are used to align the model with human intentions, making it more helpful, safe, and responsive to user instructions. This final stage is known as alignment.

- The purpose of the three training stages — pre-training, instruction fine-tuning, and reinforcement learning from human feedback (RLHF) — is to improve next-token prediction by progressively optimizing the model’s parameters. The model starts with random parameters in pre-training, which are learned from large-scale text. These parameters then serve as the foundation for instruction tuning, which makes the model better at following human instructions. Finally, RLHF further refines the model using human preferences. While parameters are updated during each stage, hyperparameters (like learning rate or batch size) are set before training and tuned separately.

- Parameters are the model's learned weights updated during training, while hyperparameters are predefined settings like learning rate or batch size that guide how training is done.

#### Instruction Fine-tuning

- During instruction fine-tuning, we typically start from the parameters learned during pre-training. To avoid altering the original model too much, we can freeze those parameters and add small trainable modules — called adapters — which are updated during fine-tuning while the original model weights remain unchanged.

- In instruction fine-tuning, we can either train separate models for individual tasks (single-task fine-tuning), or train one model on a variety of tasks (multi-task fine-tuning) so it learns to generalize across them. The second approach — multi-task fine-tuning — is what modern large language model engineering typically uses to create broadly capable models.

- To perform instruction fine-tuning yourself, the first step is to obtain a pre-trained foundation model — such as an open-source model like LLaMA. The second step is to gather instruction-following data, which can come from publicly available datasets or be generated using existing large models like GPT-4 through a process called self-instruct, where the model creates task instructions and example completions.

#### Reinforcement Learning from Human Feedback (RLHF)

- In reinforcement learning from human feedback (RLHF), researchers often train a reward model to mimic human preferences. This model is then used in place of real humans to evaluate outputs during reinforcement learning. Some recent approaches go further by using another AI model — such as a large language model acting as a simulated human judge — to generate feedback or rankings automatically.

- In some research, the same large language model is used to evaluate its own outputs. Although it may not always generate the best answer on the first attempt, it often has the ability to reflect on its responses. By comparing multiple outputs or analyzing previous answers, the model can identify stronger or weaker responses and improve future results.

- Reward models can use multiple evaluation criteria, such as helpfulness, safety, and honesty. The importance of each criterion depends on the specific application — for example, safety may be prioritized in medical settings, while creativity might matter more in writing tasks. Designing a reward model often involves balancing these goals based on context.

#### Generative Inference as a Decision Process

- Large language models work similarly to systems like AlphaGo in that they make step-by-step decisions based on current input. In the case of LLMs, the input is a sequence of tokens, and the model generates the next token, which is then appended to form the new input. This loop creates a generative process, but each individual step can be seen as a classification problem — choosing one token from a finite vocabulary.

- In AlphaGo, reinforcement learning is straightforward because the game of Go has clear rules and a well-defined reward signal: winning or losing. In contrast, large language models operate in open-ended environments where there's no built-in scoring system. As a result, reinforcement learning for LLMs relies on human feedback, reward models, or other proxy signals to define what 'good' behavior looks like.

### LLM-Based Agents

- An AI agent based on a large language model (LLM) is an integrated system capable of making plans and taking multiple steps to achieve an external goal. It interacts with the environment by converting external inputs (such as images or system states) into text that the LLM can understand — for example, using image captioning. The LLM then analyzes the situation, makes decisions, and outputs actions, which can be translated into code to control software or even physical systems like robots. During this process, the agent can use memory (long-term knowledge or past experiences) and short-term planning, both of which can be updated dynamically to guide future actions.

### Transformer Architecture and Computation

- The process by which a large language model converts input text into an output distribution is based on the transformer architecture. It begins with tokenization, then passes the tokens through a series of transformer blocks, each containing attention and feedforward layers. The final output layer produces a probability distribution over possible next tokens.

- Tokenization converts text into tokens, and each token is then mapped to a fixed vector through a process called embedding. These token embeddings are context-independent — meaning that the word 'apple' has the same vector whether it refers to the fruit or the company. The list of tokens and their corresponding vectors is learned during pre-training and is part of the model’s parameters. In addition to token embeddings, the model also uses positional embeddings to encode the position of each token in the sequence. Early language models used hand-crafted positional encodings, but modern models typically learn positional embeddings directly from data during training, using trainable parameters.

- The next stage is the transformer block, which consists of an attention mechanism followed by a feedforward network. Attention updates each token’s embedding by considering the context — it calculates the relationships between the current token and all previous tokens (to the left, in decoder-only models like GPT), then performs a weighted combination of those embeddings. This creates a new, context-aware vector for each token. There are different ways to compute these relationships, such as using dot products of queries and keys. The feedforward layer then processes the output of attention to further refine the representation. Multiple transformer blocks are stacked to deepen the model’s understanding. Finally, the output of the last token from the final transformer block is used to generate a probability distribution over the possible next tokens.

### Explainability of LLM

- There are generally two main approaches to exploring the explainability of a large language model. The first is direct analysis of the neural network itself — such as examining embeddings, attention patterns, or neuron activations — which typically requires full access to an open-source model. The second is to ask the model to explain its own outputs in natural language. While this can be useful, it doesn't guarantee that the explanation reflects the actual internal reasoning process.

- There are multiple techniques for directly analyzing the internal behavior of a neural language model. These include identifying key input tokens that significantly influence the output — often through attention weight analysis or in-context learning dynamics; tracing the training examples that most influenced a particular output (known as data attribution); and analyzing what types of information are encoded in embeddings or specific neurons.

---

**I will continue to update this post as I take more notes throughout the course.**
