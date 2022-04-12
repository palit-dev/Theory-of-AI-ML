# Support Vector Machine
Support Vector Machine (SVM) is a classification algorithm that seeks to determine a suitable hyperplane in a N-dimensional space where N is the number of features. It seeks to implement a Maximal Marginal Classifier to maximize the Marginal Distance or the distance between the Marginal Planes. The Marginal Plane in Hard SVM are hyperplanes passing through the nearest data point in each class cluster parallel to the Decision Boundary.

The difference between Logistic Regression and SVM is the presence of Maginal Hyperplanes.

## Mathematics

![Support Vector Machine](/img/svm.png "Support Vector Machine")

Let $X_1$ and $X_2$ be two points belonging to classes $C_{-1}$ and $C_1$ respectively. Then, we can represent the hyperplane passing through the points as $y_{-1}: w^T.X_1 + b = -1$ and $y_{1}: w^T.X_2 + b = 1$. The distance between these two points can be expressed as:

$$
 y_{1}: w^T.X_2 + b = 1 \newline
- y_{-1}: w^T.X_1 + b = -1 \newline
\implies w^T.(X_2 - X_1) = 2
$$

Dividing both sides with the magnitude of $||w||$ to preserve the direction, we get,

$$
(X_2 - X_1)\hat{w} = \frac{2}{||w||}
$$

where $\hat{w}$ represents the direction of the distance vector. Thus, we have to maximize $\frac{2}{||w||}$ such that $y = -1$ if $(w^T.X + b) \leq -1$ and $y = 1$ if $(w^T.X + b) \geq 1$. 

Combining these two equation, we have to maximize $\frac{2}{||w||}$ such that $y_i(w^T.X_i + b)\geq 1$. The point to note here is that $y_i(w^T.X_i + b)\leq -1$ denotes mis-classification.

In other words, we have to minimize $\frac{||w||}{2}$ such that $y_i(w^T.X_i + b)\geq 1$.

## SVM Kernel
One Important contribution of SVM is the introduction of Kernel. SVM Kernels transform data in $N$-dimensional Space to $N+1$ or higher-dimensional Space so that it can use a decision boundary in the higher dimension to classify data in lower dimension.

### Example
Consider the following problem with 1 feature. No matter where we draw the Decision Boundary, $B_1$ or $B_2$, the classification error will be large.

![Example SVM](/img/svm-kernel-1.png "SVM Kernel Example")

Thus, we can use the polynomial transformation, $y = x^2$ to transform the data points into a higher dimension.

![Example SVM](/img/svm-kernel-2.png "SVM Kernel Example Solution")

Transformation to higher dimension allows us to define a decision hyperplane that better classifies the data. 

SVM has three types of Kernels
* Polynomial Kernel
* RBF Kernel
* Sigmoid Kernel