---
aliases:
  - Regression
  - Linear Regression
---
Linear regression is a statistical method used to model the relationship between a dependent variable and one or more independent variables by fitting a linear equation to observed data. The primary assumption in linear regression is that the relationship between the variables can be represented by a straight line.

### Key Components of Linear Regression:

1. **Linear Equation:**
   - The linear regression model is represented by a linear equation of the form:
     $Y = \beta_0 + \beta_1X_1 + \beta_2X_2 + \ldots + \beta_nX_n + \epsilon$
   - Here, \(Y\) is the dependent variable, \(\beta_0\) is the intercept, \(\beta_1, \beta_2, \ldots, \beta_n\) are the coefficients of the independent variables \(X_1, X_2, \ldots, X_n\), and \(\epsilon\) is the error term representing unobserved factors that affect \(Y\) but are not included in the model.

2. **Coefficients (Parameters):**
   - The coefficients (\(\beta\)) are estimated during the training process, and they represent the slope of the line for each independent variable.
   - The intercept (\(\beta_0\)) represents the value of the dependent variable when all independent variables are zero.

3. **Objective Function:**
   - The goal of linear regression is to find the values of the coefficients that minimize the sum of squared differences between the predicted values $(Y_{\text{pred}})$ and the actual values (\(Y_{\text{actual}}\)):
     $\text{Minimize:} \sum_{i=1}^{m} (Y_{\text{pred}_i} - Y_{\text{actual}_i})^2$

4. **Ordinary Least Squares (OLS):**
   - The most common method for estimating the coefficients is the Ordinary Least Squares (OLS) method. It minimizes the sum of squared differences between the observed and predicted values.

### Assumptions of Linear Regression:

1. **Linearity:**
   - The relationship between the dependent variable and the independent variables is assumed to be linear.

2. **Independence:**
   - Observations are assumed to be independent of each other.

3. **Homoscedasticity:**
   - Residuals (differences between observed and predicted values) should have constant variance across all levels of the independent variables.

4. **Normality of Residuals:**
   - Residuals should be approximately normally distributed.

5. **No Multicollinearity:**
   - Independent variables should not be highly correlated with each other.

### Steps in Linear Regression:

1. **Data Collection:**
   - Collect a dataset with observations of the dependent variable and corresponding values of the independent variables.

2. **Data Preprocessing:**
   - Handle missing values, outliers, and other data preprocessing steps.

3. **Exploratory Data Analysis (EDA):**
   - Explore the relationships between variables using visualizations and summary statistics.

4. **Data Splitting:**
   - Split the dataset into training and testing sets.

5. **Model Training:**
   - Use the training set to estimate the coefficients of the linear regression model.

6. **Model Evaluation:**
   - Use the testing set to evaluate the performance of the model using metrics like mean squared error, R-squared, or others.

### Example (Python - Scikit-Learn):

```python
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
import numpy as np

# Generate synthetic data
np.random.seed(42)
X = 2 * np.random.rand(100, 1)
y = 4 + 3 * X + np.random.randn(100, 1)

# Split the data into training and testing sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Initialize and train the linear regression model
model = LinearRegression()
model.fit(X_train, y_train)

# Make predictions on the test set
y_pred = model.predict(X_test)

# Evaluate the model
mse = mean_squared_error(y_test, y_pred)
print("Mean Squared Error:", mse)

# Access coefficients and intercept
coefficients = model.coef_
intercept = model.intercept_
print("Coefficients:", coefficients)
print("Intercept:", intercept)
```

In this example, a simple linear regression model is trained on synthetic data using Scikit-Learn. The model is then used to make predictions on a test set, and its performance is evaluated using mean squared error. The coefficients of the model can be accessed through the `coef_` attribute, and the intercept can be accessed through the `intercept_` attribute.

![[Pasted image 20240129141821.png]]

![[Pasted image 20240129142255.png]]