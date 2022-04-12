# Regularization
The Concept of Regularization is to introduce a peanalty term proportional to the slope in order to prevent the problem of overfitting the model to the training data when the dataset size is small.

## Ridge Regression
The loss function of Ridge Regression is given by,

$$
L(w,b) = \sum_{i=1}^N [y_i - (w.x_i + b)]^2 + \lambda ||w||^2_2
$$

The weights are given by,

$$
\hat{w}= (X^TX + \lambda I)^{-1} (X^T Y)
$$

## Lasso Estimator
The loss function of Lasso Estimator is given by,

$$
L(w,b) = \sum_{i=1}^N [y_i - (w.x_i + b)]^2 + \lambda ||w||_1
$$

## Difference between Lasso and Ridge Estimator
Ridge Regression prevents the coefficients, $\hat{w}$ from taking large values by penalizing it in the loss function. However, as $\lambda$ is increased, $\hat{w}$ tends to but not 0. Hence, Ridge Regression always considers all the features for prediction. The Lasso Regression can however, reduce $\hat{w}$ to 0 with the increase of $\lambda$. When $\hat{w} =0$ for a feature, it means that it does not provides any aid in predicting the target variable. Thus, Lasso regression can in fact help in feature selection.  