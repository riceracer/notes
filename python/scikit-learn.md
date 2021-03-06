# scikit learn

```
import sklearn
```

## Estimators

Classes that implement these methods:
* `fit(X, y)`
* `predict(X)`

Hyperparameters for an estimator can be set in the constructor or via:
* `set_params(**kwargs)`, e.g. `SVC().set_params(kernel='rbf')`

Get hyperparamers via:
* `estimator.get_params()`

Get score for the estimator:
* `score(X_test, y_test, sample_weight=None)`

## Train SVM

```
from sklearn import svm

# X_train= training features, y_train=labels, X_test= test features
classifier = svm.SVC(verbose=True)
classifier.fit(X, y)
y_pred = classifier.predict(X_test)
```

## Confusion Matrix

```
from sklearn.metrics import confusion_matrix

# classifier = model, X = features, y_true = true labels
y_pred = classifier.predict(X)
confusion = confusion_matrix(y_true, y_pred)
print(confusion)
```

## Precision, Recall, F-Score

```
from sklearn.metrics import precision_recall_fscore_support

# classifier = model, X = features, y_true = true labels
y_pred = classifier.predict(X)
prfs = precision_recall_fscore_support(y_true, y_pred)
print(prfs)
```

* Output is list of Precision, Recall, F-Score, Support for each label

# Estimators

* [Ridge](http://scikit-learn.org/stable/modules/generated/sklearn.linear_model.Ridge.html#sklearn.linear_model.Ridge) - Linear estimator with L2 normalization
** See [Shrinkage](http://scikit-learn.org/stable/tutorial/statistical_inference/supervised_learning.html#shrinkage)
* [Lasso](http://scikit-learn.org/stable/modules/generated/sklearn.linear_model.Lasso.html#sklearn.linear_model.Lasso) Linear estimator trained with L1 regularization
* [LogisticRegression](http://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html#sklearn.linear_model.LogisticRegression) 
* [SVM](http://scikit-learn.org/stable/modules/svm.html) - Support Vector Machines

## SVM

Use:
* SVC() for classification
* SVR() for regression

Tips:
* should normalize input features to have stddev=1

Hyper-parameters:
* C: penalty parameter
* kernel: 
  * 'linear'
  * 'rbf' - radial basis function + 'gamma'
  * 'poly' - polynomial + 'degree'
 

# Tools / Utils

## Cross validation Generators

See: http://scikit-learn.org/stable/tutorial/statistical_inference/model_selection.html#cross-validation-generators 

* [KFold](http://scikit-learn.org/stable/modules/generated/sklearn.model_selection.KFold.html#sklearn.model_selection.KFold) k-fold cross validation
* StratifiedKFold
* GroupKFold
* ShuffleSplit
* StratifiedShuffleSplit
* GroupShuffleSplit
* Leave...Out
* PredefinedSplit

## DictVectorizer

Can take python dicts as input, and transforms them into one-hot coding for categorical features and numerical features.

```
>>> measurements = [
...     {'city': 'Dubai', 'temperature': 33.},
...     {'city': 'London', 'temperature': 12.},
...     {'city': 'San Francisco', 'temperature': 18.},
... ]

>>> from sklearn.feature_extraction import DictVectorizer
>>> vec = DictVectorizer()

>>> vec.fit_transform(measurements).toarray()
array([[  1.,   0.,   0.,  33.],
       [  0.,   1.,   0.,  12.],
       [  0.,   0.,   1.,  18.]])

>>> vec.get_feature_names()
['city=Dubai', 'city=London', 'city=San Francisco', 'temperature']
```
