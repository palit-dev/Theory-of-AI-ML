# Dimensionality

## Curse of Dimensionality
The curse of dimensionality basically means that the error increases with the increase in the number of features. It refers to the fact that algorithms are harder to design in high dimensions and often have a running time exponential in the dimensions. A higher number of dimensions theoretically allow more information to be stored, but practically it rarely helps due to the higher possibility of noise and redundancy in the real-world data.

## Principle Component Analysis
PCA is a tool for Dimensionality Reduction by transforming independent features as a linear combination of multiple features with the maximum variance.

### Algorithm
Let $X= [x_1, x_2, \dots, x_n]$ is a feature vector where column represents an independent feature. The $y$ is not required in PCA as it involves only the features.

#### Centering
For each column in $X$ subtract the mean of the column from each observation. This centers the data on the origin.

#### Standardization
For each column in $X$, divide each observation by the mean of the column. This convers the features to mean 0 and variance 1. However, this is optional and needs to be only done if you consider features with higher variances are more important. Let the centered and may be standardized matrix be $Z$.

#### Covariance Matrix
Calculate $ZZ^T$. This forms the covariance matrix.

#### Eigen Value and Eigen Vectors
Determine the Eigen Value and Eigen Vectors of the Matrix $ZZ^T$. The Eigen Vector corresponding to the largest eigen value is PC1. Similarly, Eigen Vector corresponding to the second largest value corresponds to PC2 and so on. Let $P$ be the matrix of eigen values and $P^*$ be the matrix of Eigen Vectors arranged according to decreasing Eigen Values.

#### Projection
Let $Z^* = ZP^*$ be the new points along the PCA axes.

#### Feature Elimination
The sum of diagonal elements, $ZZ^T$ gives the total variability. $Z^*$ already has 0 mean and 1 variance. Hence, $Z^*(Z^*)^T$ directly gives the covariance matrix. The diagonal element 1 gives the variance accountability of PC1 and so on. Hence, add the variance, check the percentage of total variability it account for and drop the features which does not contribute significantly to the total variability.

## Linear Discriminant Analysis
Linear Discriminant Analysis maximizes the seperatibility between known categories so we can make the best decisions. PCA does not work here because it does not distinguish between classes. LDA does this by determining a new set of axes that maximizes the distance between the mean of each class and minimizes the variance within each class. Thus, the Fisher index is given by,

$$
J(w) = \frac{(\mu_1 - \mu_2)^2}{s_1^2 + s_2^2}
$$

where $s_1$ and $s_2$ represents the scatter. For $n$ classes, we need $(n-1)$ LDA axes. This means that the number of axes becomes independent of the number of features but rather depends on the number of classes.

### Example
Let the data be:

$$
C_1 = [(1,2), (2,3), (3,3), (4,5), (5,5)]
$$

$$
C_2 = [(1,0), (2,1), (3,1), (3,2), (5,3), (6,5)]
$$

#### Matrix Representation

$$
C_1 = 
\begin{bmatrix}
1 & 2\\
2 & 3\\
3 & 3\\
4 & 5\\
5 & 5\\
\end{bmatrix}
$$

$$
C_2 = 
\begin{bmatrix}
1 & 0\\
2 & 1\\
3 & 1\\
3 & 2\\
5 & 3\\
6 & 5\\
\end{bmatrix}
$$

#### Compute Mean of each Class

$$
\mu_1 = 
\begin{bmatrix}
3 & 3.6
\end{bmatrix}
$$

$$
\mu_2 = 
\begin{bmatrix}
3.3 & 2
\end{bmatrix}
$$

#### Compute the Scatter matrices

$$
s_1 = (n_1 - 1) Cov(C_1) = 4
\begin{bmatrix}
10 & 8 \\
8 & 7.2
\end{bmatrix}
$$

$$
s_2 = (n_2 - 1) Cov(C_1) = 5
\begin{bmatrix}
17.3 & 16 \\
16 & 16
\end{bmatrix}
$$

#### Class Scatter

$$
S_w = s_1 + s_2 = 
\begin{bmatrix}
27.3 & 24 \\
24 & 23.2
\end{bmatrix}
$$

#### Optimal Line Direction
The Optimal Line Direction is given by,

$$
v = S_w^{-1} (\mu_1 - \mu_2) = 
\begin{bmatrix}
-0.79 \\
0.89
\end{bmatrix}
$$

#### Projection of Data on the Axes

$$
y_1 = v^T C_1^T \\
y_2 = v^T C_2^T
$$

