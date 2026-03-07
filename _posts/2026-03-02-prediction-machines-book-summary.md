---
title: "Book Summary: Prediction Machines by Agrawal, Gans, and Goldfarb"
layout: post
---

![book](/assets/img/20260302/book.jpg)

**This post contains my chapter-by-chapter summary of *Prediction Machines: The Simple Economics of Artificial Intelligence* by Ajay Agrawal, Joshua Gans, and Avi Goldfarb. The summaries were generated using my [Book Page Summarizer](https://github.com/Erin-1919/book-summarizer), which extracts text from book page photos and produces structured summaries via GPT-4o.**

## Introduction

### 1. Machine Intelligence

- The current wave of advances in artificial intelligence does not actually bring us intelligence but instead provides a critical component of intelligence: prediction. Prediction is a central input into decision-making, and economics has a well-developed framework for understanding decision-making. The new and poorly understood implications of advances in prediction technology can be combined with the old and well-understood logic of decision theory from economics to deliver a series of insights to help navigate an organization's approach to AI.

- There is often no single right answer to the question of which is the best strategy or the best set of AI tools, because AIs involve trade-offs: more speed, less accuracy; more autonomy, less control; more data, less privacy. A method is provided for identifying the trade-offs associated with each AI-related decision so that both sides of every trade can be evaluated in light of an organization's mission and objectives, allowing for the decision that is best for the organization to be made.

### 2. Cheap Changes Everything

- Economics provides valuable insights into the business implications of cheaper prediction. Prediction machines will be utilized for both traditional tasks, such as inventory and demand forecasting, and new challenges like navigation and translation. The reduction in prediction costs will influence the value of other business operations.

- Organizations can leverage AI prediction tools to enhance their current strategies. As these tools become more advanced, they may even drive changes in the strategies themselves. For example, if a company like Amazon can accurately predict consumer desires, it could shift from a traditional shop-then-ship model to a proactive ship-then-shop model, delivering products before they are ordered. This transformation has the potential to significantly alter organizational operations.

- The adoption of AI-driven strategies introduces new societal trade-offs, influenced by varying needs and preferences across different countries and cultures. The book is structured into five sections to explore the layers of AI's impact, starting from prediction and extending to decision making, tools, strategy, and societal trade-offs. This comprehensive approach aims to address the multifaceted effects of AI on society.

## Part One: Prediction

### 3. Prediction Machine Magic

- Prediction involves using existing data to generate missing information. It is a process that leverages available data to produce insights or information that is not immediately apparent or available.

- Small improvements in prediction accuracy can have significant impacts. An increase from 85% to 90% accuracy reduces mistakes by one-third, while an increase from 98% to 99.9% reduces mistakes by a factor of twenty. In certain contexts, reducing mistakes by such a large factor can be transformational.

- The process of filling in missing information can make prediction machines appear magical. This is evident in technologies where machines perform tasks like object recognition, navigation with driverless cars, and translation.

### 4. Why It's Called Intelligence

- Machine learning science focuses on operational effectiveness rather than average correctness, unlike traditional statistics. This approach allows for biased predictions if they are more effective, leveraging powerful computers. This flexibility has enabled rapid advancements by utilizing rich data and fast computational resources developed in recent years.

- Traditional statistical methods depend on clearly defined hypotheses or human intuition for model specification. In contrast, machine learning can handle complex models with numerous variable interactions without needing detailed pre-specification. This allows for more intricate modeling and analysis.

- Recent advances in machine learning are considered advances in artificial intelligence for several reasons. First, systems based on machine learning techniques have the ability to learn and improve over time. Second, these systems can make significantly more accurate predictions than other methods under certain conditions, which some experts believe is a core aspect of intelligence. Third, the improved prediction accuracy allows these systems to perform tasks like translation and navigation, which were once thought to be exclusive to human intelligence. It does not take a stance on whether these advances in prediction equate to advances in intelligence, instead focusing on the implications of reduced prediction costs rather than reduced intelligence costs.

### 5. Data Is the New Oil

- Prediction machines require three types of data: training data for AI training, input data for making predictions, and feedback data to enhance prediction accuracy. Each type plays a crucial role in the functioning and improvement of AI systems.

- Data collection involves significant costs and is considered an investment. The expense is influenced by the volume of data needed and the intrusiveness of the collection process. It is essential to weigh these costs against the benefits of improved prediction accuracy. Estimating the return on investment for each data type is necessary to determine the most effective approach.

- The value of additional data is influenced by statistical and economic factors. Statistically, data has diminishing returns, meaning each new data point contributes less to prediction improvement than the previous one. Economically, the impact of adding data is uncertain but can be significant if it enables a prediction machine to surpass critical thresholds, such as usability or regulatory standards. Organizations must understand how data quantity, prediction accuracy, and value creation are interconnected.

### 6. The New Division of Labor

- Humans, even those with professional expertise, often make poor predictions in specific situations. They tend to give too much importance to prominent information and fail to consider statistical properties. Numerous scientific studies have highlighted these deficiencies across various professions. This issue was notably depicted in the movie "Moneyball."

- Machines and humans each possess unique strengths and weaknesses when it comes to making predictions. As prediction machines continue to advance, these differences become more pronounced, highlighting the complementary roles of humans and machines in prediction tasks.

- Prediction machines excel at processing complex interactions among various indicators, especially in data-rich environments. As the complexity and number of dimensions increase, human ability to make accurate predictions decreases compared to machines. However, humans have an advantage in understanding the data generation process, particularly in data-scarce settings. A taxonomy of prediction settings, including known knowns, known unknowns, unknown knowns, and unknown unknowns, helps determine the optimal division of labor between humans and machines.

- Prediction machines are scalable, reducing the unit cost per prediction as frequency increases, unlike human predictions. Humans, however, can make informed predictions with limited data due to their cognitive understanding of the world. This leads to a model of human prediction by exception, where machines handle routine predictions, but seek human input for rare or uncertain events where they lack confidence. Humans thus provide critical predictions in exceptional cases.

## Part Two: Decision Making

### 7. Unpacking Decisions

- Prediction machines are highly valuable because they can often make predictions that are better, faster, and cheaper than those made by humans. Prediction is crucial for decision making under uncertainty, which is prevalent in both economic and social contexts. However, prediction is only one part of the decision-making process, which also includes judgment, action, outcome, and various data types such as input, training, and feedback.

- Understanding decision components helps assess the impact of prediction machines on human value. While human prediction value decreases, the value of complementary human skills like data collection, judgment, and actions increases. For example, London cabbies, who spent years mastering route prediction, were not outperformed by prediction machines. Instead, these machines enhanced the abilities of other drivers, making cabbies' prediction skills less unique but allowing more drivers to compete effectively.

- Judgment is about assessing the relative payoff of each potential decision outcome.

- Judgment is crucial in decision making as it involves specifying the actual objective being pursued. With the advancement of prediction machines making predictions more efficiently, the importance of human judgment will grow. People may become more inclined to apply judgment to decisions rather than defaulting to inaction.

### 8. The Value of Judgment

- Prediction machines enhance the value of judgment by reducing the cost of making predictions, thereby increasing the importance of understanding the rewards linked to actions. However, determining the relative payoffs for various actions in different scenarios is costly, requiring time, effort, and experimentation.

- Many decisions are made under uncertainty, such as deciding to carry an umbrella or authorizing a transaction. In these situations, it is crucial to evaluate the payoffs of incorrect decisions as well as correct ones, which increases the cost of assessing the payoffs for a decision due to uncertainty.

- When there are a limited number of action-situation combinations for a decision, judgment can be transferred to prediction machines, allowing them to make decisions once predictions are generated. This process, known as "reward function engineering," facilitates decision automation. However, when there are too many combinations, especially rare ones, it becomes too costly to pre-code all payoffs, making it more efficient for humans to apply judgment after predictions are made.

### 9. Predicting Judgment

- Machines can learn to predict human judgment through examples, such as in autonomous driving. It is not feasible for humans to code every possible scenario, so systems are trained by observing numerous examples and being rewarded for accurate predictions of human actions in various situations.

- There are limitations to machines' ability to predict human judgment due to a lack of data. Humans possess unique data like individual preferences that machines do not have. This data is valuable, leading companies to pay for access through loyalty programs and free services offered by platforms like Google and Facebook.

- Machines struggle with predicting rare events. Managers often make decisions regarding mergers, innovation, and partnerships without historical data on similar events. Humans rely on analogies and models to navigate these unique situations, whereas machines lack the ability to predict outcomes in scenarios that have not been frequently encountered.

### 10. Taming Complexity

- Enhanced prediction allows decision makers, both human and machine, to manage more complex scenarios by considering more "ifs" and "thens," leading to improved outcomes. This capability is exemplified in navigation, where prediction machines enable autonomous vehicles to function in uncontrolled environments, such as city streets, by learning to predict human actions rather than relying on pre-coded responses. This is also seen in airport scenarios, where predictions help determine optimal departure times, reducing unnecessary early arrivals and waiting times.

- Without effective prediction, decision makers often resort to "satisficing," which involves making decisions that are merely "good enough" based on the available information.

- People are accustomed to satisficing in both business and social contexts, which involves settling for solutions that are good enough given the available information. This approach will be challenged by prediction machines capable of handling complex decisions with multiple variables. These machines will make it less necessary to rely on solutions like airport lounges, which are currently used to mitigate the uncertainty of travel schedules. Similarly, the reliance on biopsies in medical practice, which compensates for limitations in predictive accuracy, will diminish as prediction machines improve. Both airport lounges and biopsies serve as risk management strategies, but prediction machines promise to offer more effective methods for managing risk.

### 11. Fully Automated Decision Making

- The introduction of AI into tasks does not equate to full automation. Prediction is just one aspect, and human judgment is often still necessary. However, judgment can sometimes be encoded or learned by machines, allowing them to perform actions. When machines handle all aspects of a task, full automation is achieved, removing humans from the process entirely.

- Tasks most likely to be fully automated are those where automation yields the highest benefits. This includes tasks where other components are already automated except for prediction, such as in mining; tasks where quick responses to predictions offer high returns, like in driverless cars; and tasks where reducing prediction waiting times is highly beneficial, such as in space exploration.

- Autonomous vehicles on city streets can cause accidents that affect individuals not involved in the decision-making process, creating significant externalities. In contrast, accidents on mine sites only impact those associated with the mine. Government regulations target activities that generate such externalities, posing a barrier to full automation in areas where these externalities are significant.

- Economists use the assignment of liability to internalize externalities, addressing the problems they cause. There is an expected surge in policy development regarding liability assignment due to the growing demand for automation across various new sectors.

## Part Three: Tools

### 12. Deconstructing Work Flows

- AI tools are typically designed as point solutions, each generating a specific prediction and performing a specific task. Many AI startups focus on developing a single AI tool tailored for a particular function.

- Large corporations consist of workflows that transform inputs into outputs, composed of numerous tasks. When implementing AI, companies deconstruct workflows into tasks, estimate the ROI for AI solutions, rank them, and implement from the top down. While some AI tools can be integrated easily, realizing significant benefits often requires reengineering entire workflows. This process is akin to the personal computer revolution, indicating that productivity gains from AI will take time to manifest in many businesses.

- An example of AI's impact on workflow is a hypothetical AI that ranks MBA applications. To maximize its benefits, a school would need to redesign its workflow, removing manual ranking tasks and enhancing marketing efforts. The AI would improve predictions and reduce evaluation costs, leading to changes in scholarship and financial aid offerings due to increased certainty in applicant success. Additionally, the school would adjust other workflow elements to enable instantaneous admission decisions.

### 13. Decomposing Decisions

- Tasks should be broken down to identify where prediction machines can be integrated. This process helps estimate the benefits and costs of enhanced predictions. Once reasonable estimates are made, AI tools should be ranked by ROI from highest to lowest, implementing them as long as the expected ROI is justified.

- The AI canvas assists in the decomposition process by providing structure and discipline. It requires clarity on the necessary data types: training, input, and feedback. It also demands precise articulation of prediction needs, judgment for assessing actions and outcomes, and understanding of possible actions and outcomes.

- Prediction is central to the AI canvas, necessitating identification of the core prediction for tasks. This often leads to existential discussions about the organization's true objectives. Specificity in predictions is crucial, as seen in examples like defining "best" students or profit maximization. Companies may need to revisit and refine their mission statements to align their AI strategies with their core objectives.

### 14. Job Redesign

- A job consists of various tasks, and the use of AI tools can lead to automation of some tasks previously done by humans. This can alter the sequence and importance of the remaining tasks and result in the creation of new tasks, thereby changing the overall composition of a job.

- AI tools can enhance jobs by adding capabilities, as seen with spreadsheets and bookkeepers, where AI aids in data management and analysis, thereby augmenting the role.

- AI tools can also reduce the number of jobs, particularly in environments like fulfillment centers, where automation can handle tasks more efficiently than human workers.

- AI can transform jobs by reshaping their structure, adding new tasks while eliminating others, as demonstrated in the field of radiology, where AI assists in diagnostic processes.

- AI tools can alter the focus on specific skills needed for certain jobs, such as those of school bus drivers.

- AI tools can change the value of certain skills, affecting who is best suited for particular jobs. For bookkeepers, spreadsheets reduced the importance of quick calculator skills while increasing the importance of asking the right questions to leverage technology for scenario analyses.

## Part Four: Strategy

### 15. AI in the C-Suite

- C-suite leadership should not completely delegate AI strategy to the IT department because AI tools can significantly impact organizational strategy beyond mere task productivity. AI can drive strategic change when three conditions are met: there is a fundamental trade-off in the business model, such as shop-then-ship versus ship-then-shop; this trade-off is affected by uncertainty, where potential higher sales are counterbalanced by costs from returns due to customer purchase unpredictability; and an AI tool that effectively reduces uncertainty can shift the balance of these trade-offs.

- C-suite leadership is crucial for AI strategy because implementing AI tools in one area can impact other parts of the business. For example, transitioning to a ship-then-shop model may lead to vertical integration into the returns collection business, requiring significant redesign of workflows and the firm's boundaries.

- Prediction machines enhance the value of complements like judgment, actions, and data, potentially altering organizational hierarchies. They allow managers to focus on higher-level goals aligned with organizational objectives. Owning AI-driven actions can offer competitive advantages, enabling traditional businesses to capture AI value. However, new entrants might leverage AI for competition by integrating vertically.

### 16. When AI Transforms Your Business

- Determining the boundary between your business and others is a crucial strategic decision, influenced by uncertainty. Prediction machines help reduce this uncertainty, thereby affecting how organizations define their boundaries, such as in partnerships or outsourcing.

- Prediction machines enhance the ability to write contracts by reducing uncertainty, encouraging companies to outsource tasks related to data, prediction, and action. However, they reduce the incentive to outsource tasks requiring judgment, as judgment is difficult to quantify and monitor. As AI spreads, the need for human judgment will increase, leading to more in-house employment and less outsourcing of labor.

- AI will boost the motivation to own data, but in cases where the predictions from data are not crucial, it might be more efficient to buy predictions directly. This approach avoids the need to purchase data and generate predictions internally when they are not strategically vital.

### 17. Your Learning Strategy

- Shifting to an AI-first strategy involves deprioritizing what was previously considered the top priority. This shift is not merely a trendy term but signifies a genuine tradeoff. An AI-first strategy necessitates a reallocation of focus and resources, emphasizing the importance of data strategy in enhancing prediction machines, even at the expense of immediate customer experience or employee training.

- AI can disrupt industries because incumbent firms often lack the economic incentives that drive startups to adopt new technologies. Initially, AI-enabled products may be inferior because they require time to learn and improve beyond the capabilities of hard-coded devices. Once deployed, AI can surpass competitors by continuously learning and enhancing its performance. Established companies might be tempted to adopt a wait-and-see strategy, but this can be risky as they may struggle to catch up with competitors who advance in AI training and deployment.

- Timing is crucial when releasing AI tools. Initially trained in-house, AI tools learn faster when exposed to real-world conditions and larger data volumes. Early deployment accelerates learning but increases risks, such as brand damage or customer safety issues with immature AI. In some cases, like Google Inbox, the benefits of rapid learning outweigh the downsides of poor initial performance. However, in areas like autonomous driving, the stakes are higher, and the decision to release early involves weighing the potential advantages against the significant risks of premature deployment.

### 18. Managing AI Risk

- Predictions from AI systems can result in discrimination, which poses a liability risk even if the discrimination is unintentional. This highlights the importance of ensuring that AI predictions are fair and unbiased across different groups.

- AI systems struggle with sparse data, leading to quality risks, especially in scenarios where predictions are confidently made but incorrect. This issue is particularly problematic in cases of "unknown knowns," where the confidence in predictions does not match their accuracy.

- Incorrect input data can deceive prediction machines, making them susceptible to hacker attacks. Ensuring the integrity and accuracy of input data is crucial to protect AI systems from such vulnerabilities.

- The diversity of prediction machines, similar to biodiversity, involves a trade-off between individual and system-level risks. Balancing these risks is essential to optimize the benefits of AI while minimizing potential downsides.

- Prediction machines are vulnerable to interrogation, which can lead to intellectual property theft and allow attackers to identify weaknesses. This poses significant security risks.

- Manipulating feedback can cause prediction machines to learn and adopt destructive behaviors. This highlights the importance of ensuring accurate and secure feedback mechanisms.

## Part Five: Society

### 19. Beyond Business

- The rise of AI introduces numerous societal choices, each involving trade-offs. Although AI technology is still developing, three significant trade-offs are evident at the societal level.

- The first trade-off involves productivity versus distribution. While some fear AI might make society poorer, economists agree that technological advancements improve overall well-being and productivity. AI will clearly boost productivity, but the issue lies in wealth distribution. AI could worsen income inequality, particularly by taking over specific tasks.

- The second trade-off involves balancing innovation and competition. AI technologies benefit from scale economies and increasing returns, where better prediction accuracy attracts more users, generating more data that further improves accuracy. This cycle incentivizes businesses to develop prediction machines but can lead to monopolization. While rapid innovation offers short-term societal benefits, it may not be ideal for long-term social welfare.

- The third trade-off is between performance and privacy. AI systems perform better with more data, allowing for personalized predictions, but this often reduces privacy. Some regions, like Europe, prioritize privacy, creating environments where citizens can control their data, potentially fostering a dynamic market for private information. However, this can cause friction and disadvantage European firms in competitive markets where data access is crucial.

- Jurisdictions must carefully balance these trade-offs by designing policies that align with their strategic goals and the preferences of their citizens.
