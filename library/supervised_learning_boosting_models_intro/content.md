---
title: Intro
author: Thinkful
team: grading
time: 5
uuid: 276a114a-70a2-4ddc-a1e7-da573cbf9f4a
---

In this module we'll introduce boosting, a type of ensemble modeling very popular for its flexibility and predictive power. Many a Kaggle competition has been won using boosting! Specifically, in this section we'll cover:

 * Boosting vs other ensemble methods
 * Gradient boosting
 * Boosting with classifier and regression problems

Let's get started!


## What is boosting?

Nearly every time we've introduced a new model, we've asked you to play with it to see if you can increase its predictive accuracy.  You've tried all sorts of tweaks by now: New features, dropping features, adjusting the fitting algorithm, adding or subtracting thresholds, etc.  Optimizing models this way involves trial and error, and a lot of time.  There has to be a better way!

In fact, there is, and you've already encountered it briefly.  Ensemble models combine many less effective models  (“weak learners”) into one more effective model (“strong learner”).  Random forests are a type of bagged ensemble model where many models are run in parallel and their outputs are aggregated.  Another class of ensemble models, **Boosting Models**, models the data over and over, each time adjusting the model based on what was learned from the previous one.

The boosting approach is exceptionally flexible – it works for classification and regression, and can be combined with any of the modeling approaches we've covered so far.  The principle behind boosting is iterative. We start by fitting a simple model on all the data.  We identify the information that the model was not able to account for (incorrect predictions in classifier, and residuals in regression) and build a new simple model that targets that new pool of information.  We repeat this until we reach some predetermined stopping rule.  The combination of all the models is then used to make the final predictions.

Boosting is great because we can use many simple models that are each computationally fast to arrive at very accurate predictions.  There are many different implementations of boosting that vary along the following axes:

 * **Type of simple model**. You can use almost any model you like.

 * **Index of error**. You can use residuals from regression, classification errors, or any cost function.

 * **How the next iteration targets the error**. You can weight inaccurately-predicted cases high and accurately-predicted cases low, you can directly model residuals, or you can model only the subset of the data that was inaccurately predicted.

 * **Stopping rule**. You can stop once you've run a certain number of models, once the amount of variance explained by the most recent iteration of the model is lower than some threshold, or once the change in weights between the two most recent model iterations is lower than some threshold.

Clearly there are many different ways to do boosting.  In the next assignment, we'll cover the most commonly-used implementation: gradient boosting.


