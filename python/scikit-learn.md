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
  * SVC() for classification
  * SVR() for regression
  * should normalize input features to stddev=1
