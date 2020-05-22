# Regression

## Regularization

### Ridge vs Lasso

Ridge (L2)

- Shrinks all the coefficients by the same proportion
- Differentiable so gradient descent can be used for optimization
- For data with correlation between features and labels
- Gives better performance

Lasso (L1)

- Shrinks some coefficients to 0
- Produces a sparse model 
- Performs feature selection
- Increases model explainability

# Tree-based Methods

## Decision Trees

### Regression Trees

1. Grow a large tree using recursive binary splitting - at each split, choose j and s that results in the minimum sum of RSS at each node. Stop when each terminal node has fewer than a threshold number of observations.
2. Use cost complexity pruning - vary alpha (which controls the trade-off between complexity and fit to training data) to create subtrees with different number of terminal nodes
3. Perform K-fold cross validation to estimate test MSE and pick the alpha that minimises MSE

However, the decision tree algorithm suffers from high variance (i.e. if it is fitted on different samples of a dataset, the result is very different). 

## Bagging

Bagging, or bootstrapped aggregation, seeks to lower the variance by taking repeated samples from the same training set.

- For regression tasks, prediction is made by averaging the observations.
- For classification tasks, prediction is made by taking a majority vote (i.e. the most commonly occurring class).

Test error can be estimated by taking the estimations of observations that were not fitted on the model (i.e. out-of-bag observations).

Variable importance can be measured by recording the total amount that the RSS is decreased due to splits over a given predictor, average over all B trees. A large value means an important variable. 

## Random Forest

Bagging is a subset of random forest, which at each split, selects m predictors from all p predictors. In bagging, we use all predictors at each split (i.e. m=p). This makes the trees less similar since in bagging, most of the trees will use the strong predictor in the top split.

## Boosting

Boosting works by using information from previously grown trees to modify the next tree. Namely, it pays more attention to observations giving prediction error.


# Evaluation Metrics

## Regression 

Mean squared error vs Mean absolute error vs Root mean squared error

- Measures how far the errors are from the observations
- MSE penalizes large errors more than small errors 
- RMSE gives the same unit as the original data so it is easier to comprehend

Root mean squared error vs Root mean squared logartithmic error

- When there are outliers, RMSE can explode the error to a high value. However, RMSLE scales down the error and is less affected by the outlier.
- RMSLE penalizes underestimation of the actual observation more than its observation. This is significant in business use cases where the underestimation has more dire consequences than the overestimation.

Adjusted R-squared

- Modified R-squared that is adjusted for the number of predictors in the model
- Increases only when the new term improves the model more than chance would

## Classification

True positives vs False negatives

- TP: actual positive, predicted positive
- FP: **actual negative, predicted positive**
- TN: actual negative, predicted negative
- FN: **actual positive, predicted negative**

1. Accuracy 

Accuracy = no. of correct predictions / total no. of prediction s

- If the dataset is highly skewed, the accuracy gives a false sense of achieving a good accuracy. The high accuracy could be due to correctly classifying most of the majority class but few of the minority class.

2. True positive rate (sensitivity)

Sensitivity = TP/(FN+TP)

- Proportion of positive data points that are correctly classified as positive (e.g. proportion of people with the disease who are identified as positive)
- Important in medical context

3. False positive rate (specificity)

Specificity = FP/(FP+TN)

- Proportion of negative data points that are incorrectly classified as positive (e.g. proportion of people without the disease who are identified as negative)

4. Area under curve 

- A plot of True Positive Rate against False Positive Rate of the range [0,1]
- The greater the value of AUC, the better the model

5. Recall

Recall = TP/(TP+FN)

6. F1 score

- Harmonic mean between precision and recall 
- The higher the F1 score, the better the MODEL
- High precision but low recall model gives a high accuracy but misses a large number of instances that are hard to classify


# Other important concepts

### Normalization vs Standardisation

Try standardisation for these cases and normalization otherwise:

- Unsupervised learning
- Features are close to a normal distribution
- Outliers are present


### Bias-variance trade-off

Bias

- Difference between average prediction and value we are predicting
- High bias models pay little attention to training data and overgeneralize the model
- Leads to high training and test error
- Models with high bias: linear regression 

Variance 

- Variability of model prediction of a given data point
- High variance models pays a lot of attention to the current set of observations and are unable to generalize well on unseen data
- Leads to low training error rate but high test error rate

The trade-off 

- Simple models have high bias and low variance while complex models have low bias and high variance 
- The trade-off between overfitting and underfitting the data
