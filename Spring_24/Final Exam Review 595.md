

# Midterm 1 Review

## [Exam 1 Review](../Spring_24/midterm_review.pdf)
- Math background
	- Normal distributions, variance, covariance
	- Basic matrix operations
- Machine learning process
- Hyper parameter tuning
- Feature engineering
- Data normalization
- Overfitting and underfitting
	- Bias and Variance
	- Cross-validation
	- Regularization
		- L1 and L2
	- Loss Functions
		- Mean Squared Error
		- Binary Cross Entropy
	- Gradient Descent
		- "vanilla", stochastic, mini-batch
- KNN Classifier
	- Distance measures
- Nearest Centroid Classifier
- Decision Trees
	- Information Theory
- Perceptron
- Linear Regression
- Polynomial Regression
- Logistic Regression
- Artificial Neural Networks
	- Structure
	- Back Propagation

### Covariance
$$
\begin{matrix}
var(x_1) & cov(x_n, x_1) \\
cov(x_n, x_z) & var(x_n) \\
\end{matrix}
$$

- Diagonal elements: the variance of a single dimension
- Off diagonal elements: The covariance between those two features
- Always symmetric
- Feature 1 and 2 have high covariance means when 1 goes up, so does 2
- Feature 1 and 2 have high negative covariance means when 1 goes up, 2 goes down
### Overfitting, Underfitting, and Cross Validation
- Test set vs. Validation set
	- Test is held out during model development, it is used to evaluate the system after all hyper-parameters have been tuned. Validation set is held out during model training, but used to evaluate during hyper-parameter tuning and model selection
- Bias and variance trade-off relates to model complexity:
	- Simpler model = more bias, less variance
	- Complex models = less bias, more variance
- How to decrease potential overfitting in K-Nearest Neighbors algorithm?
	- Increase k
- How to decrease potential overfitting in polynomial regression
	- Choose smaller degree
	- Add regularization

### Linear, Polynomial, and Logistic Regression
- How does an objective function relate to the weights of our model?
	- The objective function determines the loss for a particular choice of weights
	- We can plot it, and it is a plot of model weights versus the loss of the corresponding model
- Why do we want where the gradient is zero?
	- That is the minimum value of our objective function(loss function), which tells us where the best model weights are
- Analytical solution for an objective function that is convex? Intuition behind the solution?
	- Take the derivative, set the equation to 0, and solve for theta. This is equivalent to finding the values of theta that minimize the objective
	- A convex function has a single global minimum which is where the derivative is zero.
- Why want objective function to be convex?
	- For a global minimum
- Binary Cross Entropy and when is it used?
	- It's a loss function, and is used primarily for binary classification
- Mean Squared Error and when is it used?
	- It's a loss function, and is primarily used for regression

### Gradient Descent
- What is an epoch?
	- An iteration over the entire dataset
- What are you descending in gradient descent?
	- The loss function (to find the minimum)
- How do you know which direction to descend?
	- Move in the direction of the negative gradient
- End result of the gradient descent?
	- The model weights that (ideally) minimize the objective function
- Difference between standard gradient descent and mini-batch gradient descent?
	- Standard gradient descent calculates loss over the entire dataset before updating. Mini-batch gradient descent calculates loss over a subset of the data (a batch) before updating.
- Why use mini-batch instead of standard gradient descent?
	- Mini-batch is useful for large datasets because iterating over the whole dataset is time consuming and you can get a 'good enough' estimation with batch size.
- How is stochastic gradient descent different from standard ("vanilla") gradient descent?
	- Stochastic G.D estimates the error with a single sample, and takes a step after each sample
- What are the advantages and disadvantages
	- This is good because lots of steps during training, good for large datasets. Bad because the estimate of error is inaccurate, and may move in the wrong direction.
- Why do we use learning rate during gradient descent?
	- Learning rate scales the step size (weight update)
	- When the gradient is very large, it can prevent us from overstepping the minimum
	- When the gradient is very small, it can help us arrive at a good solution faster

### Regression
- Why do we add bias when performing regression?
	- It shifts our hyperplane off of 0
	- It controls the height of our hyperplane
	- This is important because we don't assume our data is centered at 0
- Why don't we assume a Bernoulli distribution in regression problems?
	- Bernoulli distributions assume values are one of two values, but in regression tasks values are real-valued
- What is the relationship between maximum likelihood estimation and binary cross entropy?
	- Binary cross entropy was derived using the maximum likelihood estimation of Bernoulli distributed data
- Why is linear regression an inappropriate method for solving classification problems?
	- Linear regression assumes there is a linear relationship between dependent and independent variables, which is not the case for classification problems
- Given that *b* indicates the bias, *$x_{01}$* indicates the value of sample 0 dimension 1, $x_{12}$ indicates the value of sample 1 dimension 2, and so on. Write the matrix that results from 3rd degree polynomial basis function to the following data matrix. (I expect values to be written as an expression/equation)
$$
\begin{matrix}
b & x_{01} & x_{02} \\
b & x_{11} & x_{12} \\
\end{matrix}
$$
$$
\begin{matrix}
b & x_{01} & x_{02} & x_{01}^2 & x_{02}^2 & x_{01}^3 & x_{02}^3 \\
b & x_{11} & x_{12} & x_{11}^2 & x_{12}^2 & x_{11}^3 & x_{12}^3\\
\end{matrix}
$$
- Since high degree polynomials can fit more data distributions, why wouldn't you always use a high degree polynomial to fit data?
	- They are prone to overfitting
	- There may be numerical instability issues with very high degrees
### Regularization
- What is the purpose of regularization
	- To avoid overfitting
- Describe at a high level how regularization
	- Regularization attempts to minimize model weights. The purpose is to avoid overfitting (under the assumption that higher the weight values, the more complex the model which are therefore more prone to overfitting)
- Why would regularization try to minimize model weights?
	- Many regularizers assume that higher the weight values, the more complex the model which are therefore more prone to overfitting
- What is the different between L1 and L2 regularization?
	- L1 regularization is the sum of absolute value of weights
	- L2 regularization is the sum of squared weights
### Information Theory and Decision Trees
- How do decision trees handle numeric data? You may give an example to explain your answer
	- By finding split point between classes, and thereby converting the data into binary features
- [[Major benefit of decision trees is that they are highly interpretable]]: ==True==
- [[A major benefit of decision trees is that they can handle categorical data]]: ==True==
- [[Information depends on context and surprise]]: ==True==
- [[A KNN classifier makes few assumptions about the distribution of the data]]: ==True==
- How is information gain used in decision trees?
	- Used to determine the optimum features to split on in a decision tree
- What is the purpose of a max depth hyperparameter in decision trees?
	- To prevent overfitting
- [[Given the following equations for entropy, calculate the entropy of the following dataset]]
- If a dataset has an entropy of 1, what does that tell you?
	- There is an even class distribution in the dataset, meaning we will need exactly one bit (heads or tails) to communicate an outcome. In other words, the outcome is a 50/50.
- Conversely, if a dataset has an entropy of 0, what does that tell you?
	- Everything in the dataset is the same class, meaning we will need zero bits to communicate an outcome. Since the outcome is always the same, there is no surprise, and therefore no information
### Artificial Neural Networks
- What is an artificial neuron? Describe it pictorially and label all components
![[artifical_neuron.png]]
- What is the function it computes?
$$h = \frac{1}{1 + e^{-\sum_{i=1}^d \theta_i * x_i}}$$
- What does it mean that an ANN is a universal approximator?
	- That it can approximate any function arbitrarily well
- How does the number of neurons in the hidden layer relate to bias and variance?
	- More neurons = more inflection points = more potential to overfit = higher variance, lower bias
	- Less neurons = less inflection points = less potential to overfit = lower variance, higher bias
- What is backpropagation?
	- Short answer (ok): The algorithm is typically used to update weights in a neural network
	- Long answer: It is an algorithm to efficiently compute the derivative of each weight in a neural network. It is derived primarily using chain rule. The derivative of each weight is used to update it during training, which is typically gradient descent. In which case, each weight is updated by moving in the direction of the negative derivate scaled by the learning rate.
- Can I use regularization with a neural network?
	- Yes, this is often called "weight" decay for neural networks
- Can I use a neural network for regression? If so, how?
	- Yes, use a linear activation function the output layer
- Given that the update formula for a weight is: $$gradient_j = z_i * h_j(1-h_j) * (\sum_{m=1}^m \theta_{k,m} * e_m)$$
	- And: $error \ of \ neuron \ 3, e_3 = \hat{y} - y$
	- Given the following neural network with neurons 1, 2, and 3, show the equation for the weight update for $\theta_{1,1}$
![[artificial_neural_network.png]]
$$gradient_{1,1} = x_1 * h_1(1-h_1) * (\theta_{1,2} * (\theta_{2,3} * (\hat{y} - y)) + \theta_{1,3} * (\hat{y} - y))$$

- My neural network has a logistic activation function in its final layer. The network is trained to predict if emails are Spam or Ham (not spam). I encode my classes as 1 = Spam, 0 = Ham
	- Given a sample, the network outputs a 0.6
	- What is the probability that the sample is Ham?
		- 1 - 0.6 = 0.4
### Perceptron
- Is a perceptron a linear classifier?
	- Yes
- How does a perceptron deal with non-linearly separable data?
	- It doesn't. A perceptron will not converge to a solution for non-linearly separable data. Furthermore, there is no guarantee that a perceptron's decision boundary gets better over time, so adding a max_epoch's parameter can stop it, but the final answer may not be any good.
### KNN
- What is "K" in a K-Nearest Neighbors Classifier, and what effect does changing it have? Relate your answer to bias and variance
	- The K-closest points to an unbalanced point "vote" on the class of a new sample.
	- Large values of K decrease variance and increase bias
	- Small values of K increase variance and decrease bias

## Hyperparameters
- KNN Classifier
	- K, Distance Measures
- Nearest Centroid Classifier
	- Distance measures
- Decision Trees
	- Splitting Criteria, Max Depth
- Perceptron
- Linear, Polynomial, Logistic Regression
	- Maybe: learning rate, momentum
	- Regularization method
	- Function: linear, logistic, polynomial degree
	- Loss Function: Binary Cross Entropy, Sum of Mean Squared Error (or Mean Squared Error)
- Artificial Neural Networks
	- Number of hidden neurons
	- Early stopping and/or regularization method




# After Midterm 1
## [[Neural Networks 2]]
- Recap: Problem Types for ANNs
- **Binary Classification:**
	- Output a scalar, the probability of true class
	- Use **sigmoid activation function** in output layer with **binary cross entropy** loss
	- **Round** the probability to convert to a label
- **Multilabel Classification**
	- Output is a vector, the independent probabilities of each class
	- Use **sigmoid activation function** in output layer with **binary cross entropy** loss
	- **Round** each probability to convert to a vector of labels
- **Multiclass Classification**
	- Output is a vector, the joint probability over all classes
	- Use **softmax activation function** in output layer with **categorical cross entropy** loss
	- **Argmax** over all probabilities to convert to a single class
- **The Vanishing Gradient Problem**
	- $$gradient_j = z_i * h_j(1 - h_j) * e_j$$
	- For neurons in deep networks, due to the chain rule, this becomes related directly to a product of weighted derivatives of individual neurons
	- This can cause the gradient to approach 0, and for learning to slow close to stopping
- **Tanh function**
	- $$f(x) = tanh(x) = \frac{2}{1+e^{-2x}} - 1$$
	- tanh function is often used instead of logistic
	- Unlike logistic, its range is -1 to 1. This is a greater range meaning that is if often steeper.
		- This means it has a higher gradient which can reduce the vanishing gradient problem
- **ReLu Function**
	- Just like tanh and logistic, ReLu is nonlinear, so it can be used in nonlinear regression problems
	- Not truly differentiable, but differentiable in practice
		- If input <= 0, derivative is 0, else derivative is 1
	- Benefits
		- Vanishing gradient problem is solved 
		- Derivative is really fast to calculate
		- Sparsity of activations (many neurons go to 0)
			- This means that less calculations are made (commonly up to 50% of a network)
			- This means deep neural networks are faster to predict and train
	- Problems
		- Instead of vanishing, gradients can explode (**exploding gradient problem**)
		- "**Dying ReLu problem**" - Because of the sparsity, whole portions of the network stop responding to input during training and training effectively stops
- Activation Functions: Take Aways
	- All of these activation functions are OK, and choice of a function typically has a small impact on performance
		- but **using a logistic function is generally a bad choice for hidden layers**
	- You can mix and match activation functions in your network
	- I recommend using **SiLU or GeLu as a default for hidden layers**
	- The activation function of the output layer is determined by the problem type and loss function
		- **Logistic for Binary Classification and Multilabel classification**
		- **Softmax for multiclass classification**
		- **Linear (No activation function) for regression**
- Optimization Algorithms
	- " define how you update at each step
	- All " work "like gradient descent"
		- you are searching a space defined by weights and loss
		- You move in the direction of the derivative
	- Each algorithm is a slight variation
		- Different claims on how they overcome challenges in the optimization function
- Common Optimization Algorithms
	- These algorithms use batch-based updates
	- The differences between them are technical and aren't important
		- Gradient descent
		- Gradient descent with Momentum
		- RMS Prop
		- AdaGrad
		- Adam (**ada**ptive **m**oment)
## [[Evaluation Measures and Imbalanced Datasets]]
- Different problem types:
	- Regression, binary classification, multiclass classification, multilabel classification
- How to construct and interpret a confusion matrix
	- This can help with error analysis
	- The error types can be used to derive new evaluation metrics
- How to evaluate the performance of a model using a variety of metrics
	- Accuracy, F1, precision, ROC curves
	- macro vs. micro measures
- We should always compare against
	- A majority class baseline for classification, mean baseline for regression
	- and if possible against some other a simple baseline (which you implement)
### Dealing with Imbalanced Data
- Learning on severely imbalanced datasets can be difficult
	- Classifiers can learn to just predict everything as the majority class
- This can be hard to overcome, however there are a few simple methods:
	1. Add class weights
	2. Artificially balance the dataset
		- Under-sample majority class
		- Over-sample minority class
		- Generate synthetic data for the minority class (SMOTE)

#### Option 1: Add Class Weights
- We can add class weights to make samples of different classes contribute more or less to loss
- By default, the class weight balances the contribution of each class

#### Option 2: Artificially Balance the Dataset
1. Under-sample the majority class
	- Randomly select a fixed number of samples from each class such that the resulting dataset is balanced
	- Problem: you are removing data which may be informative to the system
2. Over-sample the minority class
	- Randomly repeat a fixed number of samples from each minority class such that the resulting dataset is balanced
	- Problem: you are repeating data which makes those points artificially more important. What if the points are outliers?
$$Training\_Loss = J(\theta) = -\frac{1}{n}\sum_{i=1}^n loss(\hat{y_i},y_i)$$
3. Generate Synthetic Data for the minority class
	- This is typically a better option than over-sampling, but could be problematic if your synthetic data is not representative of your real data.
	- A popular data generation method is “Synthetic Minority Oversampling Technique” (SMOTE)
	- The authors recommend a combination of under-sampling the majority class and using SMOTE to over-sample the minority class. Stating that it outperforms doing only under-sampling or doing only over-sampling. 

#### SMOTE "Synthetic Minority Oversampling Technique"
- SMOTE works by:
1. For a single point, find the k-nearest neighbors and randomly select one
2. For each feature
	1. Find the difference between the sample and the its neighbor
	2. Randomly generate a number between 0 and 1 and multiply it by the difference
	3. Add the scaled difference to the feature value of that original point
- This effectively creates new features values somewhere on a line between the point and its nearest neighbor
- "This approach effectively forces the decision region of the minority class to become more general."
#### Notes on Class Weights and Artificially Balancing the Dataset
- It is best, if possible, to learn with the original data distribution
- Potential Drawbacks:
	- Class weights/oversampling can give excessive importance to outliers
		- So, for severely imbalanced datasets, you may not want to reweight/sample so that all classes are equally weighted in the loss calculation
	- Under-sampling can eliminate import datapoints
		- Particularly if the samples for a class are already sparse
	- When you modify the dataset, you learning something that is not representative of the real world.
		- Weighting or balancing the dataset biases the system
			- If you are unsure of a sample, maybe you should classify it as the majority class rather than giving equal “weight”
#### Implementation Detail: Stratified Sampling
- When you have severely imbalanced data, it is important to use stratified sampling for train/validation/test splits and cross-validation
- Stratified sampling ensures a similar class distribution per split
	- E.g. if the dataset is 95% negative, and 5% positive, then each fold of cross validation will have a 95%-5% class balance
	- This is done by sampling each class independently
- Stratified sampling is more complex for multi-label problems, and the exact solution is unclear

## [[Feature Engineering]]


## [[Weak Ensemble and Dropout]]


## [[Deep Learning]]


# [[Machine Vision and Convolutional Neural Networks]]


# [[Natural Language Processing]]


# [[Recurrent Neural Networks]]




