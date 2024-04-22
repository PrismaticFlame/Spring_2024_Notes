# [Evaluation Measures and Imbalanced Datasets PDF](../Spring_24/eval_measures_imbalanced_datasets.pdf)
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
## Precision and Recall Tradeoff
There is a trade-off between precision and recall
There is typically a threshold you can adjust the trade-off

- High Recall = Fishing with a big net
- High Precision = Spear fishing

- As you increase the size of your net, you catch more fish
- You'll catch a lot of what you wanted, but you'll get increasingly more by catch

## F-Measure
 = F1 Measure = F Score
 $$\text{F1} = 2 * \frac{precision * recall}{precision + recall}$$
 - “Harmonic mean” between precision and recall A measure that balances the trade-off between precision and recall Range: (0,1); 1 is best
## F "Beta" Measure
$\text{F}_{\beta}$ Measure
$$\text{F}_{\beta} = (1 + \beta^2) * \frac{precision * recall}{\beta^2 * precision + recall}$$
Generalized F-Measure 𝑝𝑟𝑒𝑐𝑖𝑠𝑖𝑜𝑛 ∗ 𝑟𝑒𝑐𝑎𝑙𝑙 𝛽 ∗𝑝𝑟𝑒𝑐𝑖𝑠𝑖𝑜𝑛 +𝑟𝑒𝑐𝑎𝑙𝑙 You can weight the importance of precision and recall in your metric by changing β
- β = 2 weights recall more
- β = 0.5 weights precision more
- Good to know, but F1-Measure is most commonly used

## Precision and Recall (PR) Curve
- Plots the trade-off between precision and recall
- Area under the Curve (AUC) quantifies performance with a single number
	- Higher AUC means better, more robust system (less trade-off between precision and recall)
- Generate by varying some threshold with some interval
	- For example, threshold of a logistic function output
- The optimum threshold is the Euclidean distance from the perfect model
	- E.g. Euclidean distance between (1,1) and (recall, precision) of the threshold
- The look of PR Curves can vary a lot
- There isn’t a 1-to-1 relationship between precision and recall, and the plot can be jagged.
- Plotting a majority class baseline is useful for interpretation
	- It will be a line at the positive class percentage

## Receiver Operating Characteristic (ROC) Curve
- Plots the trade off between:
	- True Positive Rate (Recall) and False Positive Rate
		- Equivalent to Sensitivity vs. 1 - Specificity
		- Lots of names for the same measures
- Area Under the ROC Curve (AUROC) can be used to quantify performance with a single number
	- Higher AUROC means better system (less trade-off between TP rate and FP rate)
- Generate
- Use with Caution: research shows that ROC Curves are misleading (overly optimistic) for problems with a high class imbalance. For these problems, precision and recall curves are preferred

# Multiclass/label Evaluation
|                | Predicted Class 1 | Predicted Class 2 | Predicted Class 3 |
| -------------- | ----------------- | ----------------- | ----------------- |
| Actual Class 1 | 4                 | 50                | 1                 |
| Actual Class 2 | 10                | 290               | 65                |
| Actual Class 3 | 0                 | 10                | 2                 |
- Show the count of samples classified as each class
- The example tells us that there is:
	- There is confusion between classes 1 and 2
	- Most of class 3 is being classified as class 2

- For Multiclass classification and Multilabel classification evaluation:
	- Report evaluation metrics for each class/label individually
	- Report Micro and/or Macro averaging between all classes
- Macro Averaged Precision, Recall, F1 
	- All classes contribute equally
	- Equally weights the performance of each class 
	- Tells us the average performance over all classes
- Micro Averaged Precision, Recall, F1
	- Classes with large number of samples dominate
	- Equally weights the performance of each sample
	- Tells us the performance over all samples
## Macro Averaging
...It's just the average of the metric for each class
- Macro Averaged Accuracy
$$\frac{1}{C}\sum_i^C Accuracy_i$$
- Macro Averaged Precision
$$\frac{1}{C}\sum_i^C Precision_i$$
- Macro Averaged Recall
$$\frac{1}{C}\sum_i^C Recall_i$$
- Macro Averaged F1
$$\frac{1}{C}\sum_i^C F1_i$$
## Micro Averaging
![[micro_averaging.png]]

- For multiclass problems (when each sample belongs to exactly 1 class), micro precision = micro recall = micro accuracy
- This is **not** the case for multi-label problems
	- One sample may have multiple labels, and a sample may have NO labels
- Consider the following True (Y) and Predicted ($\hat{Y}$) labels

# Other Evaluations Measures
- There are a lot of evaluation measures
- Common Regression Problem evaluation measures
	- Mean Squared Error (MSE)
	- Root-Mean-Squared-Error (RMSE)
	- Mean-Absolute-Error (MAE)
	- $R^2$ = Coefficient of Determination
- Common Ranking Algorithm Measures
	- Precision at K
	- Mean average precision
	- Example of ranking systems are information retrieval and recommendation systems
# Compare Against Baseline Systems
- Majority class baseline for classification
	- Classify everything as the majority class
- Mean baseline for regression
	- Output the mean of the data for every sample

