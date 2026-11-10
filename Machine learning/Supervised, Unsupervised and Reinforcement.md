## What does Machine Learning mean?
Machine Learning is a branch of AI in which computers learn patterns from data and use those patterns to make predictions or decisions, rather than explicitly programmed with every rule.
## Supervised Learning
Type of ML in which model learns from labelled data.
labelled data means that every training example contains:
1. Input (features): What we give to the model.
2. Output (label/target): The correct answer associated with that input.
**Example: Predicting house prices**
Suppose we have this dataset:

|House size (sq. ft.)|Bedrooms|Price|
|---|---|---|
|1,000|2|₹30 lakh|
|1,500|3|₹45 lakh|
|2,000|3|₹60 lakh|
|2,500|4|₹75 lakh|

Here:

- Input features: House size and bedrooms.
- Target: House price.
- The model learns the relationship between these inputs and the price.

Now suppose we give the model a new house:

- Size = 1,800 sq. ft.
- Bedrooms = 3.

The model might predict a price of ₹54 lakh.
Notice that the model already learned from examples where the correct prices were available.
The model compares its prediction with the correct answer during training and adjusts its parameters to reduce prediction errors.

#### Types of supervised learning
##### A. Regression
Regression predicts a continuous numerical value.
Common algorithm: Linear, multiple, ridge, lasso, decision tree
##### B. Classification
Classification predicts a category or class.
example: spam or not spam, fraud or genuine.
common algo: Logistic, K-nearest, naive bayes, SVM, Decision tree, Random forest

#### Importance of supervised learning
- Used when historical examples with correct answers are available.
- Helps predict future values.
- Supports automated decision-making.
- Useful in fraud detection, medical diagnosis, credit scoring and forecasting.
- Allows performance evaluation by comparing predictions with known answers.

## Unsupervised Learning
Model learns from unlabeled data.
The model tries to discover hidden patterns, similarities, relationships or structures in the data by itself.
### Example: Customer segmentation

Suppose a shopping company has information about 1,000 customers.

|Customer|Monthly spending|Visits per month|
|---|---|---|
|A|₹5,000|10|
|B|₹5,500|12|
|C|₹500|2|
|D|₹700|3|
|E|₹15,000|20|
But the company does not know which customer belongs to which category.
An unsupervised algorithm may discover three groups:
1. Group 1: Low-spending customers.
2. Group 2: Medium-spending customers.
3. Group 3: High-spending customers.
The algorithm discovers these groups based on similarities in the data. Nobody supplied the group labels during training.
#### Major types of unsupervised learning
##### A. Clustering
Clustering means grouping similar data points together.
Example: Grouping customers based on purchasing behavior.
Algo: K-means, K-Medoids, Hierarchical Clustering
##### B. Dimensionality Reduction
Means reducing the number of features while preserving as much useful information as possible.
##### C. Association Rule Learning
It discovers relationships between items.
Example: People who purchase bread and butter frequently also purchase milk.
Used in market basket analysis and recommendation systems.
### Importance of unsupervised learning

- Useful when labelled data is unavailable or expensive.
- Discovers hidden patterns in large datasets.
- Helps businesses understand customer behavior.
- Helps identify unusual observations and potential anomalies.
- Reduces data complexity through dimensionality reduction.
## Semi-Supervised Learning
Semi-supervised learning combines supervised and unsupervised learning.
It uses:
1. Small amount of labeled data.
2. A large amount of unlabeled data.
This approach is useful when collecting data is easy but manually labeling it is expensive or time-consuming.
##### How does it work?
1. Start with a small labeled dataset.
2. Train an initial model using labeled examples.
3. Use the model to estimate labels for unlabeled examples.
4. Select sufficiently reliable predictions.
5. Use those predictions along with labeled data to improve the model.
This particular process is called pseudo-labeling.
### Real-world applications

- Medical image classification where expert labelling is expensive.
- Speech recognition.
- Face recognition.
- Text classification.
- Web content classification
### Importance of semi-supervised learning

- Reduces dependence on manually labelled data.
- Makes use of large unlabeled datasets.
- Can improve performance when labelled data is limited.
- Reduces the cost of data annotation.
## Reinforcement Learning
Agent learns by interacting with an environment and receiving rewards or penalties.
Unlike supervised learning, the model is not necessarily given the correct answer for every situation.
Instead, it learns which actions leads to better long-term reward.
### Example: Training a robot to navigate a maze

Imagine a robot placed inside a maze.

Its objective is to reach the destination.

- If it moves towards the destination: It may receive a reward.
- If it hits a wall: It may receive a penalty.
- If it reaches the destination: It receives a large reward.

Initially, the robot does not know the correct path.

Through repeated interactions, it learns which actions are more beneficial.
### Important components of reinforcement learning

There are five important terms you must understand:

|Component|Meaning|
|---|---|
|Agent|The learner or decision-maker|
|Environment|The world in which the agent operates|
|State|Current situation of the agent|
|Action|What the agent chooses to do|
|Reward|Feedback received after an action|
#### Important concepts

**A. Policy**
A policy is the strategy used by the agent to decide which action to take in a given state.
**B. Reward**
A reward is numerical feedback from the environment.
**C. Cumulative reward**
The agent often aims to maximize the total reward over time, not merely the immediate reward.
**D. Exploration vs exploitation**
- Exploration: Trying new actions to discover potentially better rewards.
- Exploitation: Choosing actions already known to produce good rewards.

### Real-world applications

- Self-driving vehicles.
- Robotics.
- Game-playing AI (Chess, Go).
- Traffic signal optimization.
- Resource allocation.
- Industrial automation.
### Importance of reinforcement learning

- Enables learning through experience.
- Helps solve sequential decision-making problems.
- Useful when actions influence future situations.
- Can optimize long-term outcomes.