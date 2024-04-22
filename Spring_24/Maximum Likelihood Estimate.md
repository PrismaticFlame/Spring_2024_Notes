Maximum Likelihood Estimation (MLE) is a statistical method used to estimate the parameters of a probability distribution by maximizing the likelihood function. It is a widely used approach in both frequentist and Bayesian statistics for parameter estimation.

### Key Concepts of Maximum Likelihood Estimation:

1. **Likelihood Function:**
   - Given a statistical model with parameters \( \theta \) and observed data \( x \), the likelihood function \( L(\theta | x) \) measures the probability of observing the data given the parameter values. It represents how likely the observed data are under the assumed model.
   - The likelihood function is typically defined as the joint probability density function (PDF) or probability mass function (PMF) of the observed data, treated as a function of the parameters.

2. **Maximum Likelihood Estimator (MLE):**
   - The Maximum Likelihood Estimator (MLE) is the set of parameter values that maximizes the likelihood function. Mathematically, it is obtained by finding the values of \( \theta \) that maximize \( L(\theta | x) \).
   - In simpler terms, the MLE seeks the parameter values that make the observed data most probable according to the assumed model.

3. **Log-Likelihood Function:**
   - In practice, it is often more convenient to work with the log-likelihood function, denoted as \( \ell(\theta | x) \), which is the natural logarithm of the likelihood function.
   - Taking the logarithm simplifies calculations and avoids numerical underflow or overflow, especially when dealing with large datasets or complex models.
   - Maximizing the log-likelihood is equivalent to maximizing the likelihood function, as the logarithm is a monotonic function.

4. **Properties of MLE:**
   - Under certain regularity conditions, MLEs possess desirable properties such as consistency, asymptotic normality, and efficiency.
   - Consistency: As the sample size increases, the MLE converges in probability to the true parameter values.
   - Asymptotic Normality: The distribution of the MLE approaches a normal distribution as the sample size becomes large, making it amenable to statistical inference.
   - Efficiency: MLEs are asymptotically efficient, meaning they achieve the Cramér-Rao lower bound and have the smallest possible variance among unbiased estimators.

### Example:

Consider a simple example of estimating the mean \( \mu \) of a Gaussian distribution with known variance \( \sigma^2 \). Given a set of observed data points \( x_1, x_2, ..., x_n \), the likelihood function for the mean parameter \( \mu \) is:

$$L(\mu | x) = \prod_{i=1}^{n} \frac{1}{\sqrt{2\pi\sigma^2}} \exp\left( -\frac{(x_i - \mu)^2}{2\sigma^2} \right)$$

The log-likelihood function is:

$\ell(\mu | x) = -\frac{n}{2} \log(2\pi\sigma^2) - \frac{1}{2\sigma^2} \sum_{i=1}^{n} (x_i - \mu)^2$

To find the Maximum Likelihood Estimator (MLE) for \( \mu \), we differentiate the log-likelihood function with respect to \( \mu \), set the derivative to zero, and solve for \( \mu \). In this case, the MLE for \( \mu \) is the sample mean of the observed data.

### Application:

Maximum Likelihood Estimation is widely used in various fields, including:

1. **Statistics:** Estimating parameters of probability distributions.
2. **Machine Learning:** Learning parameters of models such as linear regression, logistic regression, and neural networks.
3. **Econometrics:** Estimating parameters in econometric models.
4. **Signal Processing:** Parameter estimation in signal processing applications.
  
MLE provides a principled approach to parameter estimation, often yielding estimators with desirable statistical properties.