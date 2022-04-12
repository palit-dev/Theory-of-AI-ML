# Ensemble Techniques

Ensemble methods is a machine learning technique that combines several base models in order to produce one optimal predictive model.

## Types of Ensemble Techniques

1. **BAGG**ing, or Bootstrap **AGG**regating. **BAGG**ing gets its name because it combines Bootstrapping and Aggregation to form one ensemble model. Given a sample of data, multiple bootstrapped subsamples are pulled. A base ML technique is used to learn on each of the bootstrapped subsamples. After each subsample Decision Tree has been formed, an algorithm is used to aggregate over the Decision Trees to form the most efficient predictor. For regression output (continuous data), mean of all the submodel outputs are used whereas for cateogircal data, majority voting is used. *Ex: Random Forest Classifier*
   
2. The term **Boosting** refers to a family of algorithms which converts weak learner to strong learners. It uses a series of Base Learners (BLs) to learn on a subset of the dataset and then uses the rest of it as test set. The data misclassified by the Base Learner 1 are used to train the next Base Learner and so on untill either the max number of Base Learners allowed is reached or the dataset is properly classified. The final classification depends on majority voting. Ex: AdaBoost, Gradient Boost

## Random Forest Classifier

The Random Forest Classifier uses shallow decision trees as the Base Learners. The entire dataset is bootstrapped or randomly sampled into subsets. These subsets are used to train the Decision trees. During classification, the data is passed to all the decision tree models simultaneously and the final classification result depends on majority voting by the individual classifiers.

Decision Trees in general have low bias and high variance i.e., it can properly classify the data on which it has been trained but fails to classify new data. Training multiple Decision Trees with randomly sampled subset of the Data reduces the variance and hence, improves the accuracy of the model on new data i.e., Random Forests are more generalised and less prone to overfitting than Decision Trees.

## SHAP Summary Plot

In simple Base Learning Models it is very easy to determine the importance of different features and their correlation with the target variable i.e., whether it is positively correlated or negetively. However, for complex ensemble techniques, the task is not that simple. SHAP is an algorithm that tries to identify the nature of correlation between the features and the target variable.