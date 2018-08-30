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

original source: https://www.slideshare.net/gabrielspmoreira/feature-engineering-getting-most-out-of-data-for-predictive-models
