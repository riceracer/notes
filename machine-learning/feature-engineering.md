# Feature Engineering

# Data cleansing

## Missing data

* "Missing"/"Not available" category
* Imputed values:
  * global mean/mode/median assignment
  * random imputation - sample value at random from the distribution of that field
  * imputed assignment based on known variable
  * carryforward value from last known
  * regression imputation - model to predict missing values from known values

## Aggregating

* Aggregate event history into summary aggregations:
  * e.g. purchase history -> number of purchases, total purchase price, avg price, ...
  * e.g. event log -> total time per event, number of times of each event type
* Pivoted aggregations
  * Instead of single summary of events, break down aggregation per category
  * e.g. orders per category, spend per category, etc

## Numerical Features

### Imputing missing numerical features

* Mean - doesn't change the natural mean of source data
* Median - more robust to outliers
* Mode
* Model - impute values from known features. However can add some bias to the imputed column.

Tools:
* `sklearn.preprocessing.Imputer`

### Rounding

* Lossy compression - only retain most N significant digits of data
* Can be used to convert numerical features to categorical
 * e.g. percentages/iles to deciles

### Binarization

* Transform discrete or continuous values to binary
 * e.g. counts to 0/1 (1 if count >= 1, 0 otherwise)
 
Tools:
* `sklearn.preprocessing.Binarizer` - takes threshold input to select the 0/1 cutoff.

### Binning

Split continuous numerical values into fixed number of bins
* Fixed-width bin - bin assignment has uniform width in the feature scale - may lead to uneven bin counts on skewed distributions
* Quantile/Adaptive binning - analyze data distribution and assign bin thresholds to divide data evenly between bins.
* Log transform binning - can bin based log(feature value) (typically do `log(1 + value)`)
 
Tools:
* `sklearn.processing`
 
### Scaling

Some models are sensitive to scale of the data, so scale features to each have roughly the same mean and standard deviation

* MinMax Scaling - moves variable value to range of 0 to 1
    * `x' = (x - min(x)) / (max(x) - min(x))`
* Standard (Z) Scaling - moves features to have mean 0 and variance 1
    * `x' = (x - mean(x)) / var(x)`

Tools:
* `sklearn.preprocessing.MinMaxScaler`
* `sklearn.preprocessing.scale`

### Normalization

Scale individual samples (rows -not the feature columns) to be a unit vector.
* `x' = x / srqt(x_1^2 + ... + x_m^2)`
* Useful where a vector space model is assumed - text classification, clustering, or kernels comparing similarity of samples.

Tools:
* `sklearn.preprocessing.normalize`

### Interaction features

Add combinations of features to linear models to increase their complexity.
* `y = x1 + x2 + x1*x2 + x1^2 * x2^2 ...`

Tools:
* `sklearn.preprocessing.PolynomialFeatures`

original source: https://www.slideshare.net/gabrielspmoreira/feature-engineering-getting-most-out-of-data-for-predictive-models
