### AutoML

Google project to use ML to explore neural network architecture using reinforcement learning.
* https://research.googleblog.com/2017/05/using-machine-learning-to-explore.html

### Bag of Words

Feature extraction method for text: takes an input document and outputs an unordered collection of word frequencies.

* Looses context of work positioning, though you can add context with n-grams.
* Typically will remove stopwords (high-frequency words with little contextual meaning in isolation: "a", "the", ...).
* Creates a high-dimensional sparse output for a given document. Simple model is a one-hot encoding or vector frequency.

### CIFAR-10

60k 32x32 color images of 10 classes,6000 images per class.
* https://www.cs.toronto.edu/~kriz/cifar.html
* Classes: airplane, automobile, bird, cat, deer, dog, frog, horse, ship, truck

### COCO

Common Objects in Context - dataset of 300K images of 80 most common object categories.
* http://cocodataset.org/

### CSR Matrix

Compressed Sparse Row matrix - memory efficient storage for sparse matricies. (aka CRS - Compressed Row Storage).

### Feature Extraction

Transforming data, such as text and images, into numerical features that can be used by machine learning.

### Feature Hashing

Fast and space efficient way to vectorize features, e.g. instead of making a bag of words lookup map for text input, hash words directly to a vector representation.

* Avoids the sparsity/dimensionality increase of one-hot encoding
* Does not have the ability to do an exact inverse mapping of feature value to source feature.

### One-hot Coding

Encoding for categorical, non-ordinal features: given K categories, create a binary feature for each of the categories.

* Downsides: for high cardinality this results in sparse high-dimensional data.

### Penn Treebank
 
University of Pennsylvania dataset of 1 million works annotated in Treebank II style, fully tagged version of Brown Corpus.
* https://catalog.ldc.upenn.edu/ldc99t42
