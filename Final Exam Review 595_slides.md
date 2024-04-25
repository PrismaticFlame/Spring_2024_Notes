# [Slides](../Spring_24/final_exam_review_595_slides.pdf)

# What is overfitting?
- ==Overfitting relates to training error decreasing at the expense of model generalization==

# Purpose of validation data?
- Maximize training error, does not necessarily maximize generalizability
- Generalization is the goal
- Training error reports performance with respect to seen data
- Training error is often optimistic with respect to novel data
- ==Validation data allows us to estimate the model performance on novel, unseen data==
- ==It is an estimate of the model's generalizability==


# What is underfitting?
- ==Fit too simple of a model to our data==
- Model has too much bias and is therefore not sensitive enough to the data

# Bias-Variance Trade-off
- **Variance** - ==amount that your model is sensitive to the data==
	- High variance will vary a lot between runs of cross-validation
- **Bias** - ==amount of assumptions built into the model==
	- High bias will vary little between runs of cross-validation
- Complex model: high variance, low bias
- Simple model: low variance, high bias

# 5. Regularization
- ==Complex models will likely overfit our data==
- ==We want to reduce the complexity of our models==
	- Complexity relates to how large our weights are
	- Large weights indicate more of a bend
	- Weights of 0 will 'turn a bend off'
- L1: uses the L1 norm of the weight vector/==sum of absolute value of weights==
	- ==makes weights go to zero==, effectively turning off features
- L2: uses the L2 norm of the weight vector/==sum of squared weights==
	- ==weights get near zero==, but features don't turn off
- Drop Out
	- Typically in Deep Neural Networks to prevent overfitting
	- ==Adds noise to the network==
		- ==Does this by adding drop out nodes, which means setting their output to 0==
	- ==Prevents overfitting==
- Early Stopping
	- Stopping training before loss stops decreasing
	- Avoids overfitting
	- May stop too early and therefore underfit model

# 6. Gradient Descent
1. Relationship between loss function and model weights
	- ==Model weights determine the predicted values of the model==
	- ==Predicted values determine the model loss==
	- ==So, model loss is ultimately a function of the model weights==
	- This is what we descend in gradient descent, and how we find weights by minimizing loss
2. ==How Weight Updates work==
	- Start somewhere on surface defined by loss function
	- Find the direction to move
	- Move in that direction
	- Repeat previous 2 steps
3. ==Variations of Gradient Descent==
	- "Vanilla" Gradient Descent
		- Gradient is estimated using entire dataset
	- Stochastic
		- Gradient estimated using single point
	- Mini-batch
		- Gradient estimated using a subset of the data (a batch)
4. Momentum
	- Mini-batches can create rough and unstable estimations of loss
		- makes step go bad
	- Momentum can help reduce this instability
		- Can help overcome local minima 
	- ==Analogous to ball rolling down hill==
	- ==Take some of the previous direction and speed and add it to the current step==
# 7. Model Evaluation
1. Problem types in model evaluation
	- Regression - Assign a real-valued number(s) to a sample
	- Classification - Assign a class or label to a sample
	- Classification Problems:
		- Binary - each sample is a member of exactly one class
			- final output is a 0 or 1 indicating class membership
		- Multi-class - each sample is a member of exactly one class
			- final output contains exactly one "1"
		- Multi-label - each sample is a member of zero or more labels
			- final output vector contains zero or more "1's"
2. Loss Functions
	- Sum of squared error
		- ==For regression problems==
	- Mean squared error
		- ==for regression problems==
	- Binary Cross Entropy
		- ==For Binary or Multilabel Classification Problems==
	- Categorical Cross Entropy
		- ==For Multiclass Problems ==
3. Evaluation Metrics
	- Accuracy
		- ==Measures percent of predictions that were correct. Not suitable for class-imbalanced problems==
	- Precision
		- ==What percent of samples that I predict are true are actually true?==
	- Recall
		- ==What percentage of true samples am I predicting to be true?==
	- F1
		- ==A measure that balances the trade-off between precision and recall==
3a. Precision and Recall Tradeoff
- High recall = Fishing with a big net
- High precision = spear fishing
- ==As you increase the size of your net, you catch more fish==
- ==You'll catch a lot of what you wanted, but you'll get increasingly more by catch==
3b. Macro and Micro Averaging
- Micro Averaged Precision, Recall, F1
	- Classes with large number of samples dominate
	- Equally weights the performance of each samples
	- ==Tells us the performance over all samples==
- Macro Averaged Precision, Recall, F1
	- All classes contribute equally
	- Equally weights the performance of each class
	- ==Tells us the average performance over all classes==
4. Train, Test, and Validation Sets
	- Training set
		- ==Used to find model weights==
	- Validation set
		- Used to estimate model generalizability
		- ==Used during the hyperparameter tuning process==
	- Test set
		- Withheld from model training and hyperparameter tuning
		- ==Used to evaluate the performance on the final, tuned model on novel unseen data==
# 8. Artificially Balance the Data
1. Under-sample the majority class
	- Randomly select a fixed number of samples from each class such that the resulting dataset is balanced
	- Problem: you are removing data which may be informative to the system
2. Over sample the minority class
	- Randomly repeat a fixed number of samples from each minority class such that the resulting dataset is balanced
	- Problem: you are repeating data which makes those points artificially more important. What if the points are outliers?
- Generate synthetic data for the minority class
	- This is typically a better option than over-sampling, but could be problematic