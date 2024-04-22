# Machine Learning Process
- Training is only a small part of machine learning
- Data collection, feature engineering, developing a model, and model refinement take most of your time
- Collecting, cleaning, and organizing data takes a lot of time

# Dealing with Data
- Data Collection
	- Identify data sources, collect, and extract the data into some useable format
		- Data can come from multiple sources in multiple formats
			- E.g. structured databases, unstructured text, images, etc...
		- Identify data sources
		- Write scripts to collect data, and typically convert to a common format
			- For example:
				- Convert a .sql database and a .json file, and a .csv file all to .csv which can then be further processed
				- Convert .pdfs into text, and scrape web pages for text (.html to text)
				- Convert .png, .jpeg, and .tiff to a common image format
- Data Cleaning
	- Imputing missing values, removing outliers, normalizing data, removing invalid samples, etc...


## Imputation
- Handling outliers
		- Normalization and Standardization
		- Text processing to remove variation
			- Regular Expressions (RegExs)
		- Missing features can be a problem for most machine learning models
		- Values may be missing because of human error, instrument error, data corruption, combining different sources of data, etc.
		- You don't always want to remove samples that have missing features
		- Some of the imputation operations you can perform are:
			- Randomly assign a value - typically randomly choose a sample and select a value from it
			- If the fact that its missing is significant, consider assigning a "missing" numerical value(e.g. -1, or 0 when measurements are positive)
			- Assign a default value, such as the feature mean or majority
			- Assign a value from a similar sample (e.g. its nearest neighbor)
			- Interpolation – if you have data in a series such as longitudinal data, signal data, or image data you can interpolate a value based on surrounding values
			- Predict a value using regression

## Handling Outliers
- Values may be outliers because of human error, instrument error, data corruption, combining different sources of data, etc.
	- Or, the sample is actually an outlier
- Find outliers using:
	- A standard deviation threshold
	- Outlier detection algorithms such as "local outlier factor"
- Once an outlier is identified, either:
	- Remove outliers from the dataset
	- Cap the value of the feature
- Not all machine learning (ML) Algorithms are sensitive to outliers, but I think it’s a good idea to deal with them up front to give yourself flexibility in choosing a ML algorithm
	- E.g. Decision trees and SVMs are robust to outliers, but linear regression and neural networks are sensitive to outliers

## Normalization and Standardization
- Data can be normalized or standardized
	- Term usage seems to vary
- Normalize between values of 0 and 1
	- Problem if new samples are outside of training data range
- Z-Scaling Normalization
	- Mean of 0 and standard deviation of 1

## Removing Variation (Text Processing)
- **Regular Expressions(RegEx)**
- Text pattern description language used to clean, normalize, and process text
- Programming language independent, but has implementations for most programming languages
- Try it interactively on a sample before putting into code
- The pattern can be characters, digits, or special symbols to represent groups of characters, digits, etc..

## Feature Engineering (Feature extraction)
- Creating informative features from the cleaned data
- Feature Engineering (sometimes called feature extraction) is the process of creating informative features from raw data
	- Benefits of good features:
		- reduce number of features needed
			- Thereby increasing speed of training and prediction
		- Decrease the amount of required training data
		- Make a model more generalizable
		- Makes a model more adaptable to similar domains or data formats
			- The features are less tied to the specifics of a dataset
	- Developing good features typically requires:
		- Combining raw features or extracting information from raw features
		- Domain knowledge
		- Error analysis
### Basic Methods
- Encoding features
- Binning/bucketing
	- Binning/Bucketing: combining data into bins or buckets
	- Can prevent overfitting
	- Can help when features are too specific, or are too sparse
- Combining Features
	- Features may be recorded separately, but may make more sense when combined
	- Features may also be combined using mathematical operations
- Splitting Features
	- Features may be recorded as a single data value, but are more discriminative when separated
	- For example
		- Name: Sam Henry
			- Split into first and last name
### More Advanced Methods
- Text Processing / Natural Language Processing
- Signal Processing
- Image Processing / Machine Vision

### Encoding Categorical Features
- When categorical features are mutually exclusive meaning a sample may belong to only one of them, a one-hot encoding is typically used
- A one-hot encoding has a 0’s for all categories except for a single value of 1, indicating it’s category
- When multiple categorical features are not mutually exclusive, meaning a sample may have zero, one, or more of those features, a binary encoding is typically used
- A Binary Encoding is a new feature, where a sample is assigned a 1 or 0 if they do or do not have that feature.

### Data Sparsity is a problem
- Raw features may be too sparse
	- This makes learning difficult and overfitting possible
- Data sparsity can be caused by:
	- Some feature values are sparse by nature, particularly continuous values
		- Income, age, height, weight
	- Having lots of features
		- The curse of dimensionality

### The Curse of Dimensionality
- As the number of features grow, the volume of the feature space grows exponentially causing the data to become sparse
- Therefore, the amount of needed data needed often grows exponentially with the dimensionality
	- A typical rule of thumb is that there should be at least 5 training examples for each dimension in the representation
		- I used to use a rule of thumb that you need the number of dimensions squared number of samples
- Machine learning relies on detecting areas where objects form groups with similar properties
- ==In high dimensional data, all objects appear to be sparse and dissimilar in many ways==
- Peaking phenomenon states that with a fixed number of training samples, the predictive power of a classifier first increases as the number of dimensions increases, but beyond a certain dimensionality it starts deteriorating

#### One-Hot Encoding Implementation
- With Pandas: • Easy for non-numeric (text) values using pandas.get_dummies
- With numPy: • Convert to numeric categorical (dictionaries make is straightforward) • Convert from numeric categorical to one-hot with numpy.eye
- With Keras: • Convert to numeric categorical (dictionaries make is straightforward) • Convert from numeric categorical to one-hot with tf.keras.utils.to_categorical

### Image Processing to Create Features
- Extract simple features from images such as:
	- Average brightness
	- Average color
	- Count of a certain color of pixels
- More complex features
	- Requiring domain knowledge (e.g. breast cancer dataset)
	- Requiring machine vision techniques
## Feature Selection
- Selecting (or removing) features that are helpful for your end-goal
- Remember the curse of dimensionality
	- Addingnewfeatures rapidly expands the feature space, making learning, and particularly generalizing more difficult
- Feature selection is the process of selecting informative features / removing uninformative features
- Typically done via:
	1. Feature filtering = univariate feature selection
	2. Finding informative combinations of features
	3. Dimensionality reduction techniques, where the features space is compressed

### Algorithm Selection
- Some algorithms work well with uninformative features
	- Decision trees
	- Recall that at each stage, you select the most informative feature
- Other's dont
	- For example, a neural network
	- You are performing a search over the feature space, and all features are treated equally. Each feature adds to the size of the feature space regardless of whether they are informative or not. Uninformative features make search space large

### Univariate Feature Selection
- Univariate feature selection is the process of selecting or removing features without considering other features in the dataset
	- Remove features with lots of missing values
	- Remove features with low variance
		- Probably require data normalization first so that “low” has more meaning
		- If variance is really low, then it probably isn’t informative, and overfitting is possible
	- Remove unused features which are irrelevant or inappropriate. Examples are:
		- ID columns, Features that wouldn't be available at the time of prediction, maybe text descriptions
	- Remove redundant features and features left over from the feature engineering process
- Remove and select features based on their correlation with the label (classification) dependent variable (regression)

### Measures of Correlation
1. F-Measure
- Assumes data is normally distributed about a linear fit
	- Therefore, limited to linear dependencies
- ANOVA for classifcation, F-Test for Regression
	- Values range from 0 to infinity
	- Low values indicate little correlation, high values indicate high correlation
2. Mutual Information
- Measure of dependence between two variables
	- Specifically, it measures the amount of information gained from one variable by observing another variable
	- Values range from 0 to 1, 0 is independent, 1 is max dependance
	- Not limited to linear dependencies

### F-Measure vs. Mutual Information
![[fmeasure_mutualinfo.png]]

### Finding Combinations of Features
1. Use measures of statistical correlation between features
	- Features are ideally independent
		- If features are highly dependent, then the two features together provide a similar amount of information as just one of those features.
	- If features are highly dependent, then the two features together provide a similar amount of information as just one of those features.
2. Empirically try combinations of features
	- For a given set of features, calculate validation/test set performance
3. For a given set of features, calculate validation/test set performance
	- Use this alone, or look at which features go to zero and manually remove them

## Dimensionality Reduction Techniques
- " combine features to capture characteristics in fewer dimensions
- Matrix Factorization Technique
	- PCA
- Neural Network-based Techniques:
	- Auto encoders

### Principal Component Analysis (PCA)
- Principal components are uncorrelated linear combinations of the data, chosen to successively maximize variance
	- Based on Eigenvalues and Eigen vectors of the covariance matrix

### Auto-Encoder
- The first known usage of autoencoders was LeCun in 1987
- Auto-encoder
	- Self-supervised algorithm which has two parts: 
	1. Encode into a compressed representation 
	2. Reconstruct (decode) from that compressed representation
- Auto-encoder • Self-supervised algorithm which has two parts: 1. Encode into a compressed representation 2. Reconstruct (decode) from that compressed representation
	1. The input layer is encoded into the hidden layer 
	2. The hidden layer contains the compressed representation of the original input 
		- The number of nodes in the hidden layer should be much less than the number of nodes in the input layer 
	3. The output layer aims to reconstruct the input layer

## Caution with Test and Validation Sets
- Keep your training and test/validation sets totally separate 
	- Do not use the test/validation set for standardization/normalization
	- Do not use the test/validation set for feature engineering
	- Don’t use the test/validation set for dimensionality reduction methods (e.g. PCA)
- Don’t use these sets to calculate feature encodings, means, etc..
- This means, your data encodings need to be saved to convert your test set.
	- If you are using convenience methods like pandas.get_dummies which create the encodings automatically based on the order of samples, this can cause a problem. The order of the samples in the test set is not necessarily the order of the samples in the training set
	- Are you sure you captured all categories? What happens if a test sample is out of the expected range? Has a different categorical values, etc..
- 