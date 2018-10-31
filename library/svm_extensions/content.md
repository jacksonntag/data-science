---
title: SVM extensions
author: Thinkful
team: grading
time: 30
uuid: 84989d8f-ffcd-4e20-a6ff-94383466a023
---

So far we've talked about the simplest possible version of Support Vector Machines. There are many different scenarios that make slight alterations to the model. We'll cover them from a conceptual basis and won't go through the mathematical proofs behind these alterations or fully chart out their ramifications for things like the loss function or how the algorithm iteratively finds optimal boundaries.


## Multiple Classes

So far we've only talked about using SVM as a binary classifier. If SVM only worked as a binary classifier it probably wouldn't have seen the wide adoption and use that it has. How do we extend it to cover multiple classes?

The simplest way is to do a hold-one-out form of binary classifier many many times (or for as many values as your outcome can take). Then for each category you create a binary classifier between having that category or having any other outcome. To aggregate these and create a multi-class classifier, each one has an output function to define its confidence in classification, which is related to its distance from the boundary and the weights for the accuracy of the classifier. The highest output value dominates thereby deciding the class.

Another way to do it is pairwise, where every category is compared to the others in pairs. Here the class is decided by the maximum number of wins given an observation's characteristics. So an observation is categorized under every possible pair of outcomes, and then the outcome is assigned to the one that was most common.


## SVM as Regressor

Support Vector Regression (SVR) operates much like an inversion of the classification problems we've been dealing with thus far. In classification we had a computational advantage because we were only interested in the points closest to the boundary. In regression, we instead are only interested in values far away from the prediction.

There are two major values we tune in SVR, C and epsilon. C is called the _box constraint_ and sets the penalty for being outside of our margin. Epsilon sets the size of our margin. So again much like the classification problem we gather our data and find its distance from a specified point (previously the boundary, now the prediction) and optimize the cost from observations being outside the margin. This ends up being a huge advantage of SVM for regression: you can set the sensitivity when building the model, not just after the fact.


## Clustering

SVM can also be used as an unsupervised clustering algorithm. We haven't yet talked about unsupervised learning (other than a brief foray into PCA) or what a clustering algorithm does, and we won't cover all of that here. Rather, keep this technique of defining boundaries and margins in mind when we start the next unit and discuss classifiers. It will be hugely relevant.


## So, why SVM?

SVM's primary advantage is its flexibility. It can have great visual explanatory power (linear SVC), tremendous accuracy (kernel smoothing), clustering (SVClustering), or the ability to control the specificity of training (SVR). Some of these options come at the cost of computational efficacy and explanatory power, particularly when in high dimensions when kernels get involved, but overall it remains a versatile modeling class that is capable of doing many different things very well.

