# Perceptron
Perceptrons are the building blocks of Artificial Neural Networks (ANN). It generates an output as a function of linear combination of it's real-valued inputs. A Perceptron is an algorithm for supervised learning of binary classifiers. This algorithm enables neurons to learn and processes elements in the training set one at a time. 

The Perceptron enables us to distinguish between the two linearly separable classes +1 and -1.

$$
y=
\mathrm{o}(X) = \begin{cases}
    1 & \text{if } w^T.X> 0 \\ % & is your "\tab"-like command (it's a tab alignment character)
    -1 & \text{otherwise.}
\end{cases}
$$

## Working
![Logistic Regression](/img/perceptron.png "Linear Boundary")

The inputs are fed into the summation node multiplied with the waits such that:

$$
f(x) = \sum_{i=1}^n w_ix_i + w_0
$$

The Summation is fed to the activation function that generates $+1$ or $-1$ depending on whether $f(x)>0$ or not. If the output, $o(X)$ does not matches the target value, $t(X)$ then we update the weights as per the rule,

$$
w_{i+1} = w_i + \eta (t-o)x_i
$$

where, $o$ is the output value, $t$ is the target value and $\eta$ is the learning rate.

We stop the update once the output becomes equal to the target value i.e., $o=t$

## Activation Function
Different activation functions can be used depending on the range of output value we require.

![Activation Function](/img/activation-function.png "Activation Function")

### Step Function
The Step function produces an output,

$$
\mathrm{o}(X) = \begin{cases}
    1 & \text{if } w^T.X> t \\ % & is your "\tab"-like command (it's a tab alignment character)
    0 & \text{otherwise.}
\end{cases}
$$

### Sign Function
The Sign Function produces an output,

$$
\mathrm{o}(X) = \begin{cases}
    1 & \text{if } w^T.X> 0 \\ % & is your "\tab"-like command (it's a tab alignment character)
    -1 & \text{otherwise.}
\end{cases}
$$

### Sigmoid Function
The Sigmoid Function produces the probability, $P(y=1|x)$ with a range, $[0,1]$.