---
title: Class imbalance
time: 30
---

Let's return our spam model. We had accuracy of about 89%. This sounds pretty impressive. It means we predict incorrectly roughly one time out of ten. But is that accuracy actually a good standard? It turns out not so much. This scenario is an example of a class imbalance problem, where one kind of outcome is much more common than the other, skewing the model. In this assignment we'll describe what class imbalance is and how to deal with it from a practical perspective.

## Class Imbalance

In an ideal world, your training data would contain an equal number of all possible outcomes so you can find what features truly indicate a propensity for a certain category of outcome. However, that is rarely the case.

A small imbalance in your outcome classes doesn't tend to make much of a difference. A large class imbalance, however, can hugely affect your model. That's because when one class makes up a large portion of the data, it can be pretty successful for a model to simply choose the dominant class _every time_. When you think about it, this makes sense. A rare event will have to have distinguishing traits in order to accurately predict it. If those traits that tend to define a rare event are often seen in the dominant class as well, then your model is probably going to predict the dominant class.

We can also recall the different types of errors we focused on before. For instance, if we were trying to find people who may have a deadly disease, we'd want to avoid false negatives, or Type II errors, and telling someone they were healthy when they're actually dying. If that disease is a rare event we could fall into the class imbalance problem. Another area that sees a lot of class imbalance problems is fraud detection.


## Baseline Performance

So how can we come up with a good baseline for performance? 

One of the simplest ways is through the dominant class rate. By dominant class we mean the most common outcome for our target variable. The simplest version of a classifier, like what we've talked about so far, is to just always predict that the result will be the most likely outcome.

Therefore it's useful to think about your model's success rate relative to that dominant class rate. If you predict something correctly 99% of the time, but it's 99% dominated by a single class, that isn't an impressive prediction.

In the case of our spam filter, only 13.4% of the trials were "spam", meaning that a model that always predicted "ham" would have an 86.6% accuracy rate... yet be completely useless for its intended purpose of filtering out spam. Since we can get 86.6% accuracy with a completely useless model we know we'll need to do better than that for our model to be worth anything.


## Dealing with Class Imbalance

There are a few things you can do to deal with this kind of problem.

The easiest is to just ignore it. If we really only care about the absolute accuracy of the model and our sample is representative of the population we aim to predict, this can be a reasonable strategy. Try to engineer features that strongly identify the minority class and this can turn out ok.

You can also change your sampling. If you deliberately oversample the minority class or undersample the majority class you can create a more balanced training set. This is particularly useful if the goal of your model is to correctly identify the minority class. This can also be done by creating synthetic samples to try to make your data more balanced or weighting samples to balance out your classes. Here is [one of the more popular synthetic sampling techniques](https://www.jair.org/media/953/live-953-2037-jair.pdf). Read the short abstract and introduction of that paper now and then come back.

Probability outputs offer another way to deal with class imbalance. Although Naive Bayes' probability outputs are generally inaccurate and not to be used, other models will give you a more accurate probability of a certain class. Things like logistic regression or support vector machines ("SVM") can be good at this. Instead of just taking the most likely outcome you can set up a specific cutoff or a more complex rule. In the binary case it could be going with the minority case if it has a priority greater than some threshold.

Lastly, you can create cost functions for errors. This effectively quantifies ways in which errors are not equal. You find some functional form to scale the cost of an error up or down. This can mean something like a Type II error being twice as bad as a Type I error, or a hundred times as bad, or however you choose to quantify that relationship. SKLearn's Naive Bayes model does not have an easy built-in way to do this, but it's a good thing to keep in mind and something we'll use later in the course.