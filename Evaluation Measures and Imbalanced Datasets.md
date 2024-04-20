# Data Balance
- Breast Cancer Dataset
	- 458 benign and 241 malignant
		- Fairly balanced (~2 to 1)
- Iris Dataset
	- 50 of each flower type
		- Perfectly balanced (1 to 1 to 1)
# Relationship Extraction
- Goal - relationship extraction
	- Given an electronic health record, extract relationships
## " as Sentence Classification
- Cast the problem as a sentence classification task
- For each sentence in the document, label it with each of the relations it conatins

# Complex Problems
- Problems with multiple classes require
	- Different classification architectures
	- Different evaluations metrics
		- Metrics for each class, metrics to combine results for all classes
	- More complex error analysis
- Imbalanced Datasets require:
	- Different evaluation measures
	- May have trouble training due to class imbalance
	- Results may need to be interpreted more carefully

# Evaluation vs. Error Analysis
- Evaluation
	- Methods to quantify the performance of an algorithm
- Error Analysis
	- Methods to determine what needs to be improved to increase performance

## Evaluation Metrics
- Primary Metrics
	- Accuracy
		- Assumes a 1 to 1 class distribution, biased in favor of the majority class
	- Precision
	- Recall
	- F-measure
	- Receiver Operator Characteristic (ROC) Curves
	- Precision and Recall Curves
	- Correlation Coefficients
## Confusion Matrix
- TP = True Positive = predicted positive and is positive
- FP = False Positive = predicted positive but it is negative
- TN = True Negative = predicted negative and is negative
- FN = False Negative = predicted negative but is positive
- P = Number Positive = TP + FN
- N = Number Negative = FP + TN

|      | Predicted Negative | Predicted Positive |
|------|--------------------|--------------------|
| Actual Negative | True Negative (TN) | False Positive (FP) |
| Actual Positive | False Negative (FN) | True Positive (TP) |
## Accuracy
$$ \text{Accuracy} = \frac{TP + TN}{P + N}$$
- Measures the percent of predictions that were correct Places an equal importance on positive and negative classes Appropriate for balanced datasets Range: (0,1); 1 is best
- Accuracy assumes classes are balanced and are equally important
	- In many cases, one class is more important than another
		- Fraud detection, cancer diagnosis, intrusion detection, relationship extraction
		- In these cases, we may tolerate greater overall error, in return for better predictions of the more important class 
	- Often the classes are imbalanced
		- In these cases, the performance on the minority class is hidden by the size of the majority class

## Precision 
$$\text{Precision} = \frac{TP}{TP + FP}$$
- How good is my performance on the samples I am predicting to be true? What percent of samples that I predict are true are actually true? Range: (0,1); 1 is best
## Recall
$$\text{Recall} = \frac{TP}{TP + FN}$$
- What percentage of true samples am I predicting to be true? Am I missing a lot of true samples? Range: (0,1); 1 is best
