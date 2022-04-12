# Intermediate Statistics
## Descriptive Statistics
Descriptive statistics is a term given to the analysis of data that helps to describe, show and summarize data in a meaningful way using numerical calculations or graphs or tables. 

## Inferential Statistics
Inferential statistics predictions are made on a random sample of data taken from a population to describe and make inference about the population. It basically allows you to make predictions by taking a small sample instead of working on whole population.

## Percentiles, Quantiles and Quartiles
Quantiles are points in a distribution that relate to the rank order of values in that distribution. It divides the data into equal parts in a sorted manner. 

* 2-Quantile value is the Median i.e., 50% of the Data lie below the 2-Quantile or median.
* 3-quantiles are called Tertiles i.e., 33.33% of the Data lie below the 1st Tertile.
* 4-quantiles are called Quartile i.e., 25% of the data lie below the 1st Quartile.
* 100-quantiles are called Percentiles i.e., 1% of the data lie below the 1 percentile.

### Inter Quartile Range
In descriptive statistics, the interquartile range tells you the spread of the middle half of your distribution.

Quartiles segment any distribution that’s ordered from low to high into four equal parts. The interquartile range (IQR) contains the second and third quartiles, or the middle half of your data set.

![Interquartile Range](/img/iqr.png "Interquartile Range")

### Box Plot
It is a visualization often used to detect outliers

![Parts of Box Plot](/img/Box-Plot.png "Parts of Box Plot")

## Five Number Summary
Descriptive Statistics involes understanding the distribution and the nature of the data. Five number summary is a part of descriptive statistics that consists of five values that helps us to describe the data.

* The Minimum Value
* 25th Percentile or Q1
* 50th Percentile or Median or Q2
* 75th Percentile or Q3
* Maximum Value

### Example
Consider the `fare` feature in the following Data Summary

![Titanic Dataset](/img/data.jpg "Titanic Dataset")

* 25-Percentile is 7.9 which means 25% of the data is below 7.9
* 75-Percentile is 31 which means 75% of the data is below 31.
* There is a large differnce between 75-Percentile and Max which means that the fare feature is highly skewed.
* The median is less than the mean ($14<32$) which means that the distribution is highly skewed to the right.

## Gaussian Distribution and skewness
The pdf of a Gaussian Distribution is given as,

$$
f(x)=\frac{1}{2\sigma^2}e^{\frac{-x^2}{2\sigma^2}}
$$

* Gaussian Distribution with a longer left tail than right is called left skewed
* Gaussian Distribution with a longer right tail than left is called right skewed

## Standardization vs Normalization
Feature scaling is one of the most important data preprocessing step in machine learning. Algorithms that compute the distance between the features are biased towards numerically larger values if the data is not scaled.

Tree-based algorithms are fairly insensitive to the scale of the features. Also, feature scaling helps machine learning, and deep learning algorithms train and converge faster.

### Normalization
Normalization or Min-Max Scaling is used to transform features to be on a similar scale. The new point is calculated as:

$$
x_{new} = \frac{x - x_{min}}{x_{max}-x_{min}} 
$$

This scales the range to [0, 1] or sometimes [-1, 1]. Geometrically speaking, transformation squishes the n-dimensional data into an n-dimensional unit hypercube. Normalization is useful when there are no outliers as it cannot cope up with them. 

### Standardization
Standardization or Z-Score Normalization is the transformation of features by subtracting from mean and dividing by standard deviation. This is often called as Z-score.

$$
x_{new} = \frac{x - \mu}{\sigma}
$$

Standardization can be helpful in cases where the data follows a Gaussian distribution. It transforms a normal distribution to a Standard normal distribution with mean 0 and standard normal deviation 1.

Standardization does not get affected by outliers because there is no predefined range of transformed features. It is not bounded to a certain range.

## Markov's Inequality
Let  X  be a non-negative random variable and let c be a positive constant. Then, Markov's Inequality states that,

$$
P(X\geq c) \leq \frac{E(X)}{c}
$$

Markov's inequality is a tail bound. It gives an upper bound on a tail probability. Markov's inequality is useful because it makes no assumptions about the shape of the distribution of  X , other than specifying that the values of  X  must be non-negative. Thus for any non-negative random variable  X , the chance that  X  is at least 10 times its mean can be bounded by Markov's inequality:

$$
P(X\geq 10E(X)) \leq \frac{1}{10}
$$

## Chebyshev's Inequality
Let  X  be a random variable with expectation $\mu$ and SD $\sigma$. Then for all  $c\gt0$

$$
P(|X-\mu|\geq c) \leq \frac{\sigma^2}{c^2}
$$

This is an upper bound on the total of two tails when the tails start at equal distances on either side of the mean. inequality is useful because it makes no assumptions about the shape of the distribution of X. Chebeshev's Inequality can be used to state that the chance that  X  is at least 2 SDs away from its mean is at most  1/4

## Person Correlation Coefficient
The Person Correlation Coefficient can be expressed as,

$$
r = \frac{\sum (x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\sum (x_i - \bar{x})^2\sum(y_i - \bar{y})^2}}
$$

## $R^2$ Value
R-Squared and Adjusted R-Squared describes how well the regression model fits the data points. The value of R-Squared is always between 0 to 1 (0% to 100%).

* A high R-Squared value means that many data points are close to the linear regression function line.
* A low R-Squared value means that the linear regression function line does not fit the data well.

Mathematically, the $R^2$ value is described as:

$$
R^2 = 1-\frac{SS_{res}}{SS_{total}} = 1 - \frac{\sum (y_i - \hat{y})^2}{\sum (y_i - \bar{y})^2}
$$

$SS_{res}$ is called the Sum of the Squared Residuals or error. It is basically the sum of squared error. $SS_{total}$ is called the Sum of Squared Average Total. It is the difference between the actual value and it's mean. The $R^2$ value can be negative if the best fit line is worse than the mean line which will make $SS_{total} < SS_{res}$

## Adjusted $R^2$ Value

Suppose our Linear Regression Model is $y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \beta_3 x_3$. Everytime, a new feature is added, the Linear Regression Model tries to assign a value to $\beta_3$ in such a way that $SS_{res}$ is increased even if $x_3$ has no correlation with $y$. Hence, for multiple regression, the increase in $R^2$ does not signify a better model. This is where Adjusted $R^2$ comes into play.

$$
R_{adjusted}^2 = 1 - \frac{(1-R^2)(N-1)}{N-p-1}
$$

where,

$N =$ total Sample Size

$p =$ Number of Predictors


The $R^2_{adjusted}$ penalizes the attributes that are **not** correlated. This is because, if the predictor is actually correlated with the target variable, the $R^2$ will be much higher and the increase in p will not effect the overall $R_{adjusted}^2$.