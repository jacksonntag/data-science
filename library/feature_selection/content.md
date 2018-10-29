---
title: Feature selection
time: 30
---

Feature selection is like handing out roses on _The Bachelor_.  We want to keep the features that have the strongest connection to the outcome, while also prioritizing features that bring something unique to the table.  Unlike _The Bachelor_, our goal isn't to narrow the options down to only one ideal featurette, but to settle on the set of features that is relatively straightforward to understand, is predictively powerful, minimizes overfitting, and is relatively computationally efficient.  Feature selection is a balancing act between explanatory power and model parsimony.  Fortunately, many feature selection algorithms are available to help data scientists optimize their feature sets.

The one thing _all_ feature selection algorithms have in common is that they work better when data is separated into a training set and a test set, and feature selection is run on the training set. 

Feature selection algorithms fall into three broad groups:


### Filter methods

_Filter methods_ evaluate each feature separately and assign it a "score" that is used to rank the features, with scores above a certain cutoff point being retained or discarded.  The feature may be evaluated independently of the outcome, or in combination with it.  Variance thresholds, where only features with a variance above a certain cutoff are retained, are an example of independently evaluating features.  The correlation of each feature with the outcome can also be used as a filter method.

Filter methods are good at selecting _relevant_ features that are likely to be related to the outcome.  They are computationally simple and straightforward, but likely to produce lists of redundant features since inter-feature relationships are not considered. Because they're "cheap" to run, you might use filter methods as a first pass at reducing features before applying more computationally demanding algorithms like wrapper methods.


### Wrapper methods

_Wrapper methods_ select sets of features.  Different sets are constructed, evaluated in terms of their predictive power in a model, and performance is compared to the performance of other sets.  Wrapper methods differ in terms of how the sets of features are constructed.  Two such feature construction methods are "forward passes" and "backward passes". In _forward passes_, the algorithm begins with no features and adds features one-by-one, always adding the feature that results in the highest increase in predictive power and stopping at some predetermined threshold.  In _backward passes_, the algorithm begins with all features and drops features one-by-one, always dropping the feature with the least predictive power and stopping at some predetermined threshold.  Forward and backward pass methods are considered "greedy" because once a feature is added (forward) or removed (backward) it is never again evaluated for the model.

Wrapper methods are good at selecting _useful_ sets of features that effectively predict the outcome.  For larger sets of features, however, wrapper methods can be highly computationally intensive and are more vulnerable to overfitting than filter methods.


### Embedded methods

_Embedded methods_ also select sets of features, but do so as an intrinsic part of the fitting method for the particular type of model you're using.  This may involve _regularization_, where a "complexity penalty" is added to goodness-of-fit measures typically used to assess the predictive power of a model.  Embedded methods provide the benefits of wrapper methods but are less computationally intensive.  Different types of models will use different embedded methods.

For a deep dive into the world of feature selection algorithms, check out [An Introduction to Variable and Feature Selection by Isabelle Guyon and Andre Elisseef]( http://jmlr.csail.mit.edu/papers/volume3/guyon03a/guyon03a.pdf), in the Journal of Machine Learning Research.