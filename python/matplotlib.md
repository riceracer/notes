# Plot a bar chart with two series

```
import numpy as np
import matplotlib.pyplot as plt


def plot_metrics(x, y1, y2):
    # Show bar chart of Distinct MMSIs in RDV per month
    idx = np.arange(len(x))
    w = 0.4
    plt.figure(figsize=(12, 10))
    plt.bar(idx, y1, w, label='This Month')
    plt.bar(idx + w, y2, w, label='Cummulative')
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
