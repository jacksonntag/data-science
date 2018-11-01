---
title: What is unsupervised learning?
author: Thinkful
team: grading
time: 60
---

In the beginning of the course we divided machine learning into two overarching types. We've now thoroughly covered the first class, supervised learning, and so we are ready to move on to the second: unsupervised learning. This module will go into depth about clustering, which is one of the most common unsupervised learning approaches.

In this checkpoint, we provide a high-level introduction to unsupervised learning before digging into to specific approaches and implementations later in this module.

At the end of this checkpoint, you'll do a drill in which you distinguish between research questions that are susceptible to unsupervised learning and ones that are not.

## What is unsupervised learning?

This module is focused on unsupervised learning, but what does that really mean? 

So far we've seen a good range of what can be done with supervised learning techniques. But to use a supervised technique you have to have a lot of information about your process and understand some aspects of it pretty well. You have to have some kind of outcome you're interested in, specifically one you can observe and record.

But that isn't always the case, and it isn't always what you're interested in. Enter: unsupervised learning.

So, you have no outcome variable. Maybe you can't actually observe what you're interested in. Maybe it just isn't that kind of problem. But there's no outcome variable. Then you don't really have a training set the way we've thought about them before. Time to pack up and go home, right?

Wrong.

Unsupervised learning looks through the data you do have, a series of independent variables that make up your observed (or observable) data, and allows you to do something with it or say something about it. What can you do or say? Many different things. It depends on what kind of unsupervised model you want to build.


## Clustering

Clustering models are probably the simplest to logically grasp. Let's say you have a bunch of variables that you've observed as part of a process that you're studying. A clustering algorithm will go over that set of variables and say, "I think these are groups of related observations." 

That can happen in two ways. Typically you tell it how many groups, or clusters, the algorithm is allowed to generate, and the algorithm goes over the data creating the groups that minimize some cost function. More rarely the algorithm can find the number of groups on its own.


## Variable Importance

You've actually already worked on variable importance in this course. PCA is an unsupervised technique for finding out which variables tend to be most influential in your dataset. There are plenty of other techniques in this space, but we'll leave you with PCA for this course.

## Neural Networks

Lastly come neural networks. Neural networks get their own module later in this course, but they can function as either a supervised or unsupervised technique. Unsupervised neural networks have become an important technique, particularly in things like image recognition where it can be effective in discovering __latent variables__ which are impactful but not explicitly defined in the initial dataset.

This brief overview of techniques gives a sense of what unsupervised techniques can accomplish, but we'll dive in deeper as we introduce specific techniques throughout the module. There are many topics we won't cover in this course. You can refer to [this text](https://medium.com/intuitionmachine/navigating-the-unsupervised-learning-landscape-951bd5842df9) for a brief introduction to other techniques and [this one](http://www.inf.ed.ac.uk/teaching/courses/pmr/docs/ul.pdf) for a more in depth and technical survey. Unsupervised learning is a deep and evolving field of which we're only barely able to scratch the surface.

As we already mentioned, unsupervised learning can work in a myriad of contexts some of which operate on their own and others which are great for working in concert with other approaches (like how PCA is a great first step to building a supervised model).

## Evaluation

This is not without challenges, however. Probably the biggest difficulty in unsupervised learning is evaluation. Since there is no outcome variable, defining the accuracy of the model isn't really possible, since you have nothing to evaluate against. There are some approaches for dealing with this.

Firstly, you can look at the volatility of your model. If it stays reasonably stable to slight perturbations or the exclusion or addition of some data this is a relatively good thing.

Unsupervised learning also often has to simply be tested. If you're trying to create clusters, test what you intended to do with those clusters and see if it works as you'd hoped. Instead of working on this specific step in the data pipeline, you evaluate how later steps perform and tweak the unsupervised step to see how it affects performance.

The truth remains, however, that many of these models have no absolute form of evaluation. It can be extremely hard to say whether an unsupervised model is a 'good' or 'bad' model.

## Complexity

With the challenge of evaluation comes another: complexity. Since these models are hard to evaluate it is also often difficult to decide on a stopping condition. This leads to models that can get increasingly more complex and therefore more resource consuming to run. This is particularly true of neural networks, something we'll talk about in greater detail later.

This can be addressed through imposing some of your own limitations or keeping some of the structures simple, but it is definitely still a risk in this class of models.

There is also significant research, particularly in neural networks, that shows the advantages of some of the more complex models. Their performance can be quite strong.

## Drill

_For each of these scenarios decide if you could use supervised or unsupervised techniques, or both!_

 1. Define the likelihood that an individual will contract a specific disease
 2. Translate a set of images into variables for modeling
 3. An ecommerce company wants to identify power users
 4. That same company wants to see shopping patterns in users
 5. You want to reduce the number of variables inputting into your random forest model

If any of these scenarios are unclear feel free to follow up with your mentor.
