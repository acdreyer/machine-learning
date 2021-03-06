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

### Draft 1

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
The model is [here](toxiccomments_first_full_iteration.ipynb).


### Draft 2

The 1st draft had poor performance and additional features were added. The initial use of the hashingVectorizer with the Tfidif transform was retained, but an additional hashingVectorizer with ngrams were added. Word ngrams of up to 5 words were used, with english stopwords and a `LemmaTokenizer()` with `l1` normalization. 

`hv2 = HashingVectorizer(n_features=2 ** 18,ngram_range=(1, 5),norm='l1',analyzer='word',stop_words="english",tokenizer=LemmaTokenizer(),alternate_sign=False)`

Numerical features were also added, namely count of exclamation marks, question marks and uppercase characters. The ridge regression model was found to perform best, with parameters `alpha=5` and `normalize=True`.
The model is [here](toxiccomments_2ndDraft.ipynb).

### Final version

No significant gains could be made in the alloted time going from the 2nd draft to the final version.