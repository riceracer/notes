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

## Categorical Features

Issues:
* non-numeric so need to be mapped to numbers or vectors to be used in models
* high cardinality can cause issues (sparse encodings)
* can be difficult to impute missing values
* categories may be dynamic - new ones added after training the model
* need to consider if categories are ordinal or non-ordinal

### One-hot encoding

* Transform *m* category values into *m* binary features
    * or *m-1* binary features as to micro-optimize an implicit cateogry 
* Works for constrained categorical sets (M < 100), however doesn't scale for 100,000s of cateories (document ids, user ids, large hierarchies)
  
Tools:
* `sklearn.preprocessing.OneHotEncoder` 

### Feature hashing

* Instead of one-hot encoding, hash categorical features into vectors of fixed length (e.g. n=10, 20 or 50)
* Gives a much denser encoding than 1-hot
* Can have collisions between categories (but can tune category cardinality vs encoding length).

Tools:
* `sklearn.feature_extraction.FeatureHasher`

### Bin Counting / Category replacement

* Replace the category variable with one or more statistics representing the category
   * count/sum of category attribute (e.g. number of movies)
   * average/mean value of category (conversion rate, price, income, age)

### Rank encoding

* Replace category label with a rank of the category over some metric
    * replace product category with ad conversion rank 1, 2, 3, ...

### Category embedding / auto-encoder

* Use a neural network architecture to map category to a vector embedding (via encoder/decoder)
* Denser representation than 1-hot
* May have more meaningful dense representation than pure feature hashing

Tools
* `tf.contrib.layers.sparse_column_with_hash_bucket`
* `tf.contrib.layers.embedding_column`

## Temporal Features

### Time Zones

* May want to convert times to local time features of the event location

### Time binning

* apply binning on time of day to make it more flexible and general
* Can also apply binning to dates: day of week, weekend, month, quarter

### Time series trends

* Instead of just capturing average/total spend, quantize statistics by time buckets:
    * spend last week, last month, last quarter, last year
    * this separates declining trends from increasing ones which may have same total

### Time to events

* Factor in time to holidays or significant days in the domain to behavior
    * days to Christmas, days to nearest holiday, etc

### Time difference features

* features of date interaction
    * time between last purchase and current browsing behavior
    
## Spatial Features

### Types of spatial variables

May come originally in many forms:
* lat/lon
* street addresses
* zip codes, cities, states, etc - may need to map to raw coordinates

### Derived features

Given some spatial location, derive properties related to location:
* distance to nearest store of interest

### Spatial Enrichment

Given location, replace the location with a feature based on the location:
* depth of sea or elevation
* household median income

## Textual Data

### Text preprocessing considerations

Cleaning:
* lower/uppercasing
* accent character conversion
* removing non-alphanumeric or non-alpha chars

Tokenizing:
* encoding punctuation marks, phrases
* n-grams, skip-grams, char-grams
* affixes

Removing:
* stopwords
* rare words
* common words

Rooting:
* spell correction
* chop
* stem
* Lemmatize

Enriching
* entity insertion / extraction
* parse trees

### Text vectorization

Convert text to a fixed length feature vector (e.g. 50-128 length vector encoding)

* Bag of Words (BoW) - like 1-hot encoding for words - sparse and wide
* TF-IDF - term frequency - inverse document frequency - adds weighting of word uniqueness
* Embeddings - Word2Vec, etc., encodings built from corpuses and autoencoders
* Topic models - LDA, LSA, NMF

Tools
* `sklearn.feature_extraction.text.CountVectorizer`
* `sklearn.feature_extraction.text.TfidfVectorizer`

### Text similarity

* Token similarity: number of common tokens (or tf-idf terms) between two texts
* Edit distance: distance from one word/string to another via number of edits to transform from one to another
* Cosine Similarity: Can use cosine similarity of vectors to calculate how similar one vectorized text is to another

Tools:
* `sklearn.metrics.pairwise.cosine_similarity`


original source: https://www.slideshare.net/gabrielspmoreira/feature-engineering-getting-most-out-of-data-for-predictive-models
