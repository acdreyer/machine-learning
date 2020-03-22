# machine-learning

## Assignment 1: Wikipedia Toxic comments

This assignment entails detecting of comments that are marked any of the following
categories:
* toxic
* severe_toxic
* obscene
* threat
* insult
* identity_hate

### First draft

Firstly it seemed apparent that the data is overfit on the test data from the start, 
since high accuracies were obtained for the training data and low accuracies were
obtained for the test data. Hence strategies to reduce overfitting would be required.

For the 1st draft, experimentation was primarily done with various algorithms
to see which ones perform better using minor modifications. 

It was found that random forest severely underperformed compared to other algorithms. 
Ordinary least squares performed 2nd worst because of its high false positive
rate, even though it had comparable true positive rates than other algorithms.
It was found that least ordinary squares also take the longest to solve.
Subsequently it is recommended to drop both random forest and least squares from 
the algorithms that are used.

A primary focus was given to optimizing the HashingVectorizer feature extraction method, 
and minor increases in baseline performance was achieved by removing stopwords
from the built-in sci-kit learn english dictionary and ngram words in order to allow identification
using multiple words with the following statement:

`hv = HashingVectorizer(n_features=2 ** 18,ngram_range=(1, 5),analyzer='word',alternate_sign=False)`

Experimentation was done by adding features that count exclamation marks and question marks,
but these quantitative features had little effect on overall performance and 
was subsequently left out of the analysis.

The ridge regression was found to achieve the lowest false positive rate, with 
comparable true positive rates compared to Logistic regression, Naive bayes and 
Perceptron, but had the closest mean prediction to validation set.
Hence ridge regression was selected for the first submission.

However, it is recommended to further refine the HashingVectorizer and Quantitative
feature extraction parameters, since the overall test results is still fairly low.