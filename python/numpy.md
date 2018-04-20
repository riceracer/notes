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
