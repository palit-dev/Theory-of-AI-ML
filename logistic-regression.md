# Logistic Regression
Logistic Regression is a classification algorithm which use probability to classify new samples using continuous and discrete measurements. 

## Intuitive Idea

Suppose we want to develop a two class, $C_{-1}$ and $C_1$ classifier with a linear decision boundary that takes in $x\in R^d$ where $d$ is the number of predictors and outputs a $y\in\{-1,1\}$ representing the two classes.

![Logistic Regression](/img/logistic.png "Linear Boundary")

Hence, if we have $w$ and $b$ for the Linear Decision boundary, then for a given $x$:

$$
w.x + b > 0 \implies x\in C_1
$$

Thus, intuitively we can say that $P(y = 1 |x)$ increases as the linear function i.e., $w.x + b$ increases and is $0.5$ when $w.x+b=0$.

However, the output of the Linear Function $\in R$. So how do we convert a range $(-\inf, \inf)$ to a probability in the range $[0,1]$.

## Squashing Function
Given $z\in R$, the sqaushing function given as output in the range $[0,1]$ and 0.5 for $z=0$. It is defined as,

$$
s(z)=\frac{1}{1+e^{-z}}
$$

## Converting Logistic Regression to Probability
Hence, we can write,

$$
P(y=1|x)=\frac{1}{1+e^{-y}}=\frac{1}{1+e^{-(w.x+b)}}
$$

Similarly for the other class, we can write

$$
P(y=-1|x) = 1-\frac{1}{1+e^{-(w.x+b)}}=\frac{1}{1+e^{(w.x+b)}}
$$

Combining the above two equations we may write,

$$
P(y=k|x)=\frac{1}{1+e^{-ky}}=\frac{1}{1+e^{-k(w.x+b)}}
$$

## ML for Logistic Regression
The PMF of Logistic Regression is given by,

$$
L(w,b) = \prod_{i=1}^n P(y_i = k_i|x_1) =  \prod_{i=1}^n  \frac{1}{1+e^{-k_i(w.x_i + b)}}
$$

Using log likelihood and incroporating $b$ inside of $w$,

$$
l(w,b) = \log{L(w,b)}= \sum_{i=1}^n \ln{1+e^{-k_i(w.x_i + b)}} =\sum_{i=1}^n \ln{1+e^{-k_i(w.x_i)}}
$$

Differentiating this equation and equating it to 0 does not provide us any analytical solution. However, this is a convex function in $w$ and hence, we can use numerical methods.

## Gradient Descent
The Gradient Descent Algorithm tries to iteratively minimize the loss function. Mathematically, it is expressed as,

$$
w_{t+1} = w_t - \eta_t \nabla l(w_t)
$$

where $w_0 = 0$ and $\eta_t$ is called the learning rate.

Using the Gradient Descent, we can rewrite the ML for Logistic Regression as,

$$
w_{t+1} = w_t + \eta_t \sum_{i=1}^n y_i x_i P(y_i | x_i)
$$

### Margin of Error

The Margin of Error is given by,

$$
Margin(x) = |P(y_1 | x) - \frac{1}{2}|
$$

## Stochastic Gradient Descent
In Gradient Descent, each update takes into account contribution from all the data points, thus making it computationally expensive.

In stochastic Gradient, instead of considering all the points, we consider only 1 i.e.,

$$
w_{t+1} = w_t + \eta_t  y x P(y | x)
$$

In the next update, we consider a different $(x,y)$ and hence, keep cycling through all the points. This algorithm works better when the size of the dataset is huge.

## Mini Batch Gradient Descent
In Mini Batch Gradient Descent, instead of considering all the data points, we divide the data into subsets, $B_k$. The update rule is calculate for points belonging to a single subset and for the next update, the next batch is selected. 

$$
w_{t+1} = w_t + \eta_t \sum_{i=1, x_i y_i \in B}^n y_i x_i P(y_i | x_i)
$$