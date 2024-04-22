
# Terminology
- Weak Learner: a classification or regression algorithm that performs poorly. Usually (but not strictly) they are computationally simply. Weak learners typically are less prone to overfitting
- Ensemble Method: a method to combine the outputs of different algorithms. Ensemble methods hope to lessen the potential for overfitting
- Stacking: an ensemble method that uses the outputs of classifiers as input into another classifier
- Bagging: an ensemble method that uses bootstrap sampling to generate many models on a dataset
- Boosting: an ensemble method in which classifiers are applied sequentially, and the prediction performance of one classifier affects how the next classifier is built

# Weak Learning
Are many simple learners better than a single complex learner?

They can be, because it can prevent overfitting

**Ensemble Methods**:
1. Stacking
2. Bagging
3. Boosting

## Stacking
- Several model outputs are input into another model
- Ensemble methods can be used with any learner
- It doesn't have to be a weak learner
- Good way to combine the output of classifiers with complementary performance
	- Requires detailed error analysis
		- Confusion matrices
		- Manual analysis

## Bagging
- Bagging = Bootstrap Aggregating
- Bagging generates m new training, Di of size n’sets using bootstrap sampling
- By sampling with replacement, some observations may be repeated in each $D_i$
- Sampling with replacement ensures each Di is independent from its peers as it does not depend on previous chosen samples

- A single classifier is on each $D_i$
- This results in m models
- Given a new sample, a single output is aggregated by:
	1. averaging for regression
	2. voting for classification

- Bagging can be done with any model
- Bagging can decrease potential for overfitting
- Bagging is very common for decision trees

Advantages:
- Reduces potential for overfitting
- Very easily parallelized
Disadvantages:
- Loss of interpretability of a model
- Can be computationally expensive depending on the data set

Random Forest solves the problem of generating correlated trees

# Random Forests
- Like bagging, but we use a subset of features for each bootstrapped sample
- For each split, select m random features
	- $\sqrt{number\_of\_features}$ is a good default choice, but in general it is a hyperparameter
	- Find optimum split among those m features
	- Repeat
- This means that the possible features at each split is randomized

- Cannot overfit the data with respect to the number of trees
	- because adding trees does not increase the flexibility of the model

### Algorithm
- For each tree in the forest
	- Draw a bootstrap sample of size n' from the training data
	- Grow a random-forest tree from the bootstrapped data by recursively repeating the following steps
		1. Select m variables at random
		2. Pick the best split among the m variables
		3. Split the node into two daughter nodes
- Output the ensemble of trees
- For prediction
	- Take a majority vote (classification)
	- Average the results (regression)

### Summary
- Random forests are an ensemble method similar to bagging, but solves the problem of having identically distributed trees
- Good when no single decision trees gives the desired performance
Problems:
- When the number of variables is large and m is small, random forests tend to perform poorly
	- This is because the probability of selecting a relevant feature is small
- As with bagging, there is a loss of interpretability

# Boosting
- Turns a series of weak learners into a strong learner
- There are a variety of boosting methods, at their core most consist of iteratively:
	1. Iteratively learning weak classifiers with respect to a distribution
	2. Weighting the vote of each classifier relative to the classifier’s performance
	3. Adding their predictions to a final strong classifier. 
- Between iterations of weak learner creation the importance of each sample in the training data is reweighted based on if it was correctly or incorrectly classified

- Boosting consists of creating a series of weak learners.
- The performance of the previous learner influences the creation of the next learner
- The predictions of each learner are combined using an ensemble method (typically weighted voting)


1. Why do samples have weights?
The weight of each sample relates to the importance of correctly classifying that sample
- Initially all samples are equally important
- If a sample is correctly classified then its importance is decreased
- If a sample is incorrectly classified then its importance is increased

2. What weak learner should I use?
Typically the weak learner will make a decision based on a single feature, and most frequently decision stumps are used
- But boosting algorithm is a "meta-algorithm"
	- It sets up a framework for which different classifiers could be used

3. How (and Why) do I create a training set?
Use Weighted Bootstrap Sampling
- The idea is similar to bagging, except the dataset size does not change and we use each sample’s weight  (its importance) as the probability it will get selected for the new dataset
- The result is a dataset with more copies of important samples and less copies of unimportant samples

4. How do I weight the model?
Model weights tells the strength of the model's vote in the ensemble 
$$weight = \frac{1}{2} * log(\frac{1 - error}{error})$$

5. How do I reweight samples?
Sample weight tells how important each sample is to correctly classify
It is updated after each model is added to the boosting ensemble

For incorrectly classified samples:
	$new_{sample\_weight} = weight * e^{model_weight}$

For correctly classified samples:
	$new_{sample\_weight} = weight * e^{-model_weight}$

## Boosting Algorithms
- Adaboost
	- What these slides describe
	- Historically important, popularized the idea of boosting
- LogitBoost
- XGBoost
- Many Others

# Drop Out
- Drop out is used to prevent outfitting
- Does so by adding "noise" to the network
	- It does this by "dropping out" nodes, which means setting their output to 0

- Claims to be as effective as regularization (weight decay) without added computational complexity
- Prevents outfitting by inducing sparsity in the network
	- Meanings many weights go to zero

## Details
- Drop-out each neuron with probability (rate)
	- The original paper proposes a rate of 0.5
		- 50-50 chance a neuron is dropped out
	- More recent research states values between 0.5-0.8 work well
- Dropout is recommended for each densely connected hidden layer
	- Don’t use dropout for convolutional layers, etc..
- To ensure the the sum over inputs remains the same, the outputs of hidden layers are scale by
$$\frac{1}{(1-rate)}$$
## Training Theory
- Assuming a neural network with n neurons, each neuron may or may not be “turned off”
- Therefore, this network represents 2n possible “thinned networks”
- For each batch during training, it is highly likely that the randomly created “thinned network” will be novel. 
	- We make a prediction with this network, then backpropagate to adjust the weights
		- Neurons that were turned off did not contribute to the error, and therefore their weights are not adjusted
- So training a neural network with dropout can be seen as training a collection of 2n thinned networks with extensive weight sharing, where each thinned network gets trained very rarely, if at all.

## Prediction Theory
- During prediction, no neurons are dropped out. The prediction of this network can be viewed as the mean prediction of all possible 2n thinned networks 
- In practice, this gives very similar performance to averaging over a large number of dropout networks.
	- A network with a single hidden layer of n units and a softmax output, the output of this “mean network” is exactly equivalent to the geometric mean of the all 2 n possible networks

## Co-adaptations
Drop out prevents complex co-adaptations of neurons
- During overfitting, the model learns statistical noise
	- Specifically, given all neurons in a network, during training the goal is to minimize the loss function
- In doing so, a neuron may change it’s output to “fix mistakes” of it’s input neurons
	- This leads to complex co-adaptations, which lead to overfitting because these co-adaptions do not generalize to unseen data
- Using dropout, a neuron may be turned off
	- Therefore, neurons cannot rely on other neurons being present
	- This prevents co-adaptations because in every iteration the presence of a unit is highly unreliable
	- Instead, it forces the layers to accept their input as-is
		- i.e. a neuron will no longer try to “fix mistakes” of the input neurons because that input may not be present

## Dropout with ReLu
- There is some question of whether dropout works well with ReLu activation functions*
	- Dropout also causes neurons to “turn off ”, so maybe too many neurons get turned off?
	- However, the original dropout paper used dropout with ReLu functions, so it’s debatable.
	- However, the original dropout paper used dropout with ReLu functions, so it’s debatable.