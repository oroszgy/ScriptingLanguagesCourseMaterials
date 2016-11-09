Scikit-learn (sklearn)
======================

--------------------------------------------------------------------------------

Installation
------------

``$ sudo pip[3] install scikit-learn``

``$ conda install scikit-learn``

``$ sudo apt-get install python-sklearn``

--------------------------------------------------------------------------------

Overview
---------

1. Problem setting
2. Supervised learning
3. Unsupervised learning
4. Validation

http://github.com/jakevdp/sklearn_pycon2014

--------------------------------------------------------------------------------

Problem / Data
--------------

* Data is represented in a 2D array ``[n_samples x n_features]``
* numpy array
* Optional: target features/classes

--------------------------------------------------------------------------------

Supervised learning
-------------------

Classification
~~~~~~~~~~~~~~~

* SVM
* Log-linear models
* Nearest neighbours
* Naive Bayes
* Decision Trees
* etc.

Regression
~~~~~~~~~~

...


--------------------------------------------------------------------------------

Unsupervised learning
----------------------

* dimensionality reduction
* clustering
* matric factorization
* neural network models
* ...

--------------------------------------------------------------------------------


Estimator interface
-------------------

... is a uniform interface

Notation: ``X`` is a 2D array of data, ``y`` is an array of target labels

--------------------------------------------------------------------------------

Supervised case
~~~~~~~~~~~~~~~

* ``model.fit(X, y)`` - fit the training data
* ``model.predict(X_new)`` - predicts labels
* ``model.predict_proba(X_new)`` - predicts labels with estimated probs
* ``model.score(X_test, y_test)`` - calculates average accuracy

--------------------------------------------------------------------------------

Unsupervised case
~~~~~~~~~~~~~~~~~

* ``model.fit(X)`` - fit the  data
* ``model.transform(X)`` - transform the data
* ``model.fit_transform(X)`` - fit & transform the data

--------------------------------------------------------------------------------

Validation
----------

``sklearn.metrics`` contains methods for computing

* Classification metrics
* Multilabel rakning metrics
* Regression metrics
* Clustering metrics
* Pairwise metrics

--------------------------------------------------------------------------------

Other components
-----------------

... and much more ...

* data preprocessing
* feature selection
* model selection
* pipelining estimators
* ensemble learning
* semi-supervised learning
