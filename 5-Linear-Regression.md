# Linear Regression
A Linear Regression Model assumes that the regression function, $E(Y|X)$ is linear in the inputs, $X_1, X_2, ..., X_p$. Hence, for a given input vector, $X^T = (X_1, X_2,..., X_p)$ and predicted real-valued output, $Y$, the Linear Regression Model has the form

$$
f(X) = \beta_0 + \sum_{j=1}^{p} X_jB_j
$$

The performance of Linear Regression can be improved by understanding the following heuristics:

* **Linear Assumption:** Linear Regression assumes that the relationship between your inputs and outputs are linear in nature. It does not support anything else. Hence, you may need to transform data to make the relationship linear (e.g. log transform for an exponential relationship).
* **Remove Outliers:** Remove outliers in the output variable, $Y$ if possible. 
* **Remove Collinearity:** Linear regression will over-fit your data when you have highly correlated input variables. Consider calculating pairwise correlations for your input data and removing the most correlated.
* **Gaussian Distribution:** Linear regression will make more reliable predictions if your input and output variables have a Gaussian distribution. You may get some benefit using transforms (e.g. log or BoxCox) on you variables to make their distribution more Gaussian looking.
* **Rescale Inputs:** Linear regression will often make more reliable predictions if you rescale input variables using standardization or normalization.

## Linear Regression using Least Squares
The most popular estimation method in which we pick the coefficients, $\beta = (\beta_0, \beta_1,\dots,\beta_p)^T$ to minimize the Residual Sum of Squares (RSS). The cost function is expressed as,

$$
J(\beta) = RSS(\beta) = \sum_{i=1}^{N} (y_i - f(x_i))^2 = \sum_{i=1}^{N} (y_i - \beta_0 - \sum_{j=1}^{p} x_{ij}B_j)^2
$$

In terms of Matrices, we can define, $\beta = (\beta_0, \beta_1,\dots,\beta_p)$ and $X = (1, X_0, X_1,\dots,X_p)^T$ such that,

$$
Y = \beta X
$$

Hence, the cost function for outputs, $Y = (Y_0, Y_1, \dots, Y_n)$ can be written as,

$$
J(\beta) = ||Y - \beta X||^2 = (Y - \beta X)^T(Y - \beta X)=Y^TY-Y^T\beta X - X^T\beta^TY+ X^T\beta^T\beta X
$$

Differentiating w.r.t $\beta$, 

$$
\frac{d}{d\beta}J(\beta) = -Y^TX - (X^TY)^T + 2X^TX\beta =0
$$

$$
\frac{d}{d\beta}J(\beta) = -2Y^TX + 2X^TX\beta=0
$$


$$
\implies Y^TX = X^TX\beta 
$$

$$
\implies X^TY = X^TX\beta 
$$

$$
\implies \beta = (X^TX)^{-1}X^TY
$$

For two coefficients, the model can be simplified to,

$$
\beta_0 = \bar{y} -\beta_1\bar{x}
$$
$$
\beta_1 = \frac{\sum_{i=1}^N (x_i - \bar{x_i})(y_i - \bar{y_i})}{\sum_{i=1}^N (x_i - \bar{x_i})^2}
$$

## Multi-collinearity
The key purpose of a regression equation is to tell us the individual impact of each of the features on the dependent/target variable. So, a regression coefficient captures the average change in the dependent variable for every unit change in the explanatory variable, keeping all the other explanatory variables constant. 

However, if the features are correlated, it will not be possible to disentangle their individual effects on the target variable. Simply speaking, if feature, F1 and F2 are correlated, we cannot observe the impact of F1 on Y keeping F2 constant as any change in F1 will simultanoeously impact F2.

Thus, one of the key assumptions for a regression-based model is that the underlying features are independent.

### Solution 1
If the number of features are less, we can create a Correlation heatmap and drop those features for which the correlation is greater than 90%. 

### Solution 2
Variance Inflation Factor (VIF) allows you to determine the strength of the correlation between the various independent variables. It is calculated by taking a variable and regressing it against every other variables.

While correlation matrix and scatter plots can be used to find multicollinearity, they only show the bivariate relationship between the independent variables. VIF ,on the other hand, shows the correlation of a variable with a group of other variables.

Here is how VIF works:
Assuming you have a list of features — $x_1, x_2, \dots x_4$.
You first take the first feature, $x_1$, and regress it against the other features:

$$
x_1 \sim x_2 + x_3 + x_4 
$$

In the multiple regression above, you extract the $R^2$ value (between 0 and 1). If $R^2$ is large, this means that $x_1$ can be predicted from the three features, and is thus highly correlated with the three features — $x_2, x_3,$ and $x_4$. If $R^2$ is small, this means that $x_1$ cannot be predicted from the features, and is thus not correlated with the three features —$x_2, x_3,$ and $x_4$.

Based on the $R_2$ value that is calculated for $x_1$, you can now calculate its VIF using the following formula:

$$
VIF = \frac{1}{1-R^2}
$$

$(1-R^2)$ is also called the tolerance value. The valid value for VIF ranges from 1 to infinity. A rule of thumb for interpreting VIF values is:

* 1 — features are not correlated
* $1<VIF<5$ — features are moderately correlated
* $VIF>5$ — features are highly correlated
* $VIF>10$ — high correlation between features and is cause for concern 

The Following is a python implementation of VIF


```python
import pandas as pd
from sklearn.linear_model import LinearRegression
def calculate_vif(df, features):    
    vif, tolerance = {}, {}
    # all the features that you want to examine
    for feature in features:
        # extract all the other features you will regress against
        X = [f for f in features if f != feature]        
        X, y = df[X], df[feature]
        # extract r-squared from the fit
        r2 = LinearRegression().fit(X, y).score(X, y)                
        
        # calculate tolerance
        tolerance[feature] = 1 - r2
        # calculate VIF
        vif[feature] = 1/(tolerance[feature])
    # return VIF DataFrame
    return pd.DataFrame({'VIF': vif, 'Tolerance': tolerance})
```

