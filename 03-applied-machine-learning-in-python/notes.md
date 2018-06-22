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