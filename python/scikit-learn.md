# scikit learn

```
import sklearn
```

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
