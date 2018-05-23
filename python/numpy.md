# Numpy

```
import numpy as np
```

## Read csv line by line into arrays

You can do this for data sources were number of records per line is not uniform.
* Otherwise you should just use `pandas.read_csv` or `numpy.genfromtxt('my_file.csv', delimiter=',')`

```
filename = 'foo.csv'
with open(filename, newline='') as csvfile:
    for line in csvfile.readlines():
        npline = np.fromstring(line, sep=',')
```

## Effecient 1-by-1 generation of ndarray / stride

Build up python list of arrays, then create the ndarray at the end:

```
features = ... # 1-D array values
labels = ... 1-D array of values
feature_rows = []
label_rows = []
num_features = len(features) // len(labels)
window = 10  # number of positions per segment
for i in range(len(labels) - window + 1):
    feature_rows.append(features[i * num_features : i * num_features + window * num_features])
    label_rows.append(labels[i + window - 1])
X = np.asarray(feature_rows)
y = np.array(label_rows)
```

## Unique count of elements in an array

```
unique, counts = np.unique(y, return_counts=True)
count_list = list(zip(unique, counts))
```

## Create folds

E.g. to split input training data into equally sized non-overlapping sets:

``` 
# Optional
from sklearn import datasets
digits = datasets.load_digits()
X_digits = digits.data
y_digits = digits.target
# make folds
X_folds = np.array_split(X_digits, 3)
y_folds = np.array_split(y_digits, 3)
```

* In sklearn can also use [KFold](http://scikit-learn.org/stable/modules/generated/sklearn.model_selection.KFold.html#sklearn.model_selection.KFold)
