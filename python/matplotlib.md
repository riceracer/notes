## Mac install matplotlib

Using conda, in your target env:

```
python -mpip install matplotlib
```

## Plot a bar chart with two series

```
import numpy as np
import matplotlib.pyplot as plt


def plot_metrics(x, y1, y2):
    idx = np.arange(len(x))
    w = 0.4
    plt.figure(figsize=(12, 10))
    plt.bar(idx, y1, w, label='Series 1')
    plt.bar(idx + w, y2, w, label='Series 2')
    plt.ylabel('Count')
    plt.title('My Title')
    plt.xticks(idx + w / 2, x, rotation="vertical")
    plt.legend(loc='best')
    plt.show()
    

dates = ['2019-01', '2019-02', '2019-03', '2019-04', '2019-05']
series_a = [3, 4, 2, 5, 6]
seriea_b = [3, 7, 9, 14, 20]
plot_metrics(dates, series_a, seriea_b)
```
