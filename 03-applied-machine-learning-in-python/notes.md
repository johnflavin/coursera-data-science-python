# Week 1

## Key Concepts in Machine Learning

* **Supervised learning** Learn to predict target values from labelled data
    * **Classification** Target values are taken from a discrete set
    * **Regression** Target values are taken from a continuous set
* **Unsupervised learning** Find structure in unlabeled data
    * **Clustering** Find groups of similar instances in the data
    * **Outlier detection** Find unusual patterns

Steps in training a classifier

* Representation - Convert the input data to a form you can use to train/test your model. Could be extracting a set of features for an object.
* Evaluation
* Optimization

## Python Tools for Machine Learning

We will use `scikit-learn` for this course.

* [User Guide](http://scikit-learn.org/stable/user_guide.html)
* [API](http://scikit-learn.org/stable/modules/classes.html)

## Example Machine Learning Problem

We are training a classifier on some simple fruit feature data.

This code uses a function from scikit-learn to split a data set into training and testing data:

    from sklearn.model_selection import train_test_split
    X = fruits[['height', 'width', 'mass', 'color_score']]
    y = fruits['fruit_label']
    X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=0)

We're going to use a K-Nearest Neighbors classifier. This is an "instance" based classifier, meaning it stores the entire training set and uses it directly during testing.

> Given a training set X\_train with labels y\_train, and given a new instance x\_test to be classified:
>
> 1. Find the most similar instances (let's call them X\_NN) to x\_test that are in X\_train.
> 2. Get the labels y\_NN for the instances X\_NN.
> 3. Predict the label for x\_test by combining the labels y\_NN, e.g. simple majority vote.

KNN algorithm needs

1. A distance metric (e.g. Euclidean distance, which KNN calls Minkowski with p=2)
2. A value for k
3. Potentially a weighting for different neighbors
4. A way to combine the k labels, like voting

## Supervised Machine Learning

### Naïve Bayes

"Naïve" in the sense that they make the simplying assumption that all features are independent.

SKLearn has three flavors of naïve bayes: Bernoulli (binary features), Multinomial (discrete features), Gaussian (continuous/real-valued features). In this course we cover Gaussian only; in text mining course (part 4 in specialization) they use Bernoulli and Multinomial.

(Note for the SKLearn implementation of gaussian naïve bayes. It supports a "partial_fit" method in addition to "fit", for when data are too large to fit into memory all at once.)

Pros:

* Easy to understand
* Simple, efficient parameter estimation
* Works well with high-dimensional data
* Often used as a baseline comparison against more sophisticated methods

Cons:

* Assumption that features are conditionally independent given the class is not realistic
* As a result, other classifier types often have better generalization performance
* Confidence estimates for predictions are not very accurate

### Random Forests

An example of an "ensemble model". Combine multiple models into one, which is more accurate than consitiuent models. Average out overfitting to different parts of input data in different models.

Build a bunch of trees using randomized data splits, and randomized sets of features. The final prediction is the majority vote among trees.

Important SKLearn RandomForestClassifier / RandomForestRegressor params:

* `n_estimator`: controls number of trees
* `max_features`: controls number of features selected for each tree to fit
* `max_depth`: depth of each tree
* `n_jobs`: number of cores for parallel training

Pros:

* Widely used, excellent prediction performance on many problems
* Doesn't require careful normalization of features or extensive parameter tuning
* Like decision trees, handles a mixture of feature types
* Easily parallelized across multiple CPUs

Cons:

* Resulting models are often difficult for humans to interpret
* Like decision trees, random forests may not be a good choice for very high-dimensional tasks (e.g. text classifiers) compared to fast, accurate linear models

### Gradient Boosted Decision Trees

The "serial" tree ensemble to Random Forests' "parallel" ensemble.

Training builds a series of small decision trees. Each subsequent tree attempts to correct the errors from the previous stage.

"learning rate" controls how "hard" each new tree tries to correct remaining mistakes from previous round ("hard" in terms of complexity of the tree). Lower learning rate means training is slower, but often generalizes better.

Pros and cons similar to random forests.
