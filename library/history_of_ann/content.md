---
title: History of ANN
author: Thinkful
team: grading
time: 45
uuid: 669a0469-120f-4a66-8072-529d1c16b1ad
---

A long long time ago, in a galaxy that was actually this same galaxy, people started building artificial neural networks. Artificial Neural Networks (ANN) were, somewhat unsurprisingly, born of a desire to simulate neural networks in the brain. This work really began in the 1950s, and while it is now considered a significant development in computer science, it wasn't really seen to be that at the time.

In fact, while there were some significant developments along the way, Neural Networks faded from the general consciousness. In fact, a now very popular lecture from MIT on neural networks acknowledges that they were almost scrapped from the curriculum on Machine Learning at the school (you can see that lecture [here](https://www.youtube.com/watch?v=uXt8qF2Zzfo)). It may seem extreme now, but that was the reality a little over a decade ago. Neural Networks were ineffective and inefficient.

Now, of course, ANN has become one of the most exciting and influential facets of machine learning. _Deep Learning_ is one of the most in-demand skills in the world today, based entirely on ANN as a framework.

So, how did this happen?

### The Rebirth of Neural Networks

Most people would point to 2006 as the year that the rebirth of Neural Networks started to regain traction.

There was a series of machine learning teams starting to win several competitions (think an older, more exclusive version of Kaggle) with neural networks. A particularly famous team of researchers from this period were led by Jurgen Schmidhuber out of a lab in Switzerland called IDSIA. As what are now called neural networks started winning competition after competition, people started to take notice.

At the time, ANNs were being used as an unsupervised technique. As computational power continued to develop, however, they also became relevant for supervised learning problems. Some people started to develop ways to run these algorithms even more efficiently using things like GPUs, or Graphics Processing Units, which are highly [parallelizable](https://www.quora.com/Why-and-how-are-GPUs-so-important-for-Neural-Network-computations) and allowed for these systems to get even more complex.

To this point, however, coding up a neural network required a lot of manual development of algorithms. This limited their impact to only the most technical projects in the machine learning world.

That would soon change.

## New Tools

As with many open source tools in the past decade or so, our story now has to turn to Google. In around 2011, a team at Google started working on a tool called DistBelief. This was a key part of Google Brain, one of Google’s earlier Artificial Intelligence projects, and became the back end for several different internal projects.

When DistBelief became more and more impactful, Google chose to make it open source in 2015 in a new iteration, now known as TensorFlow. TensorFlow is a robust tool set for building a variety of models, but it is particularly useful for neural networks. 

Initially, TensorFlow was relatively complex to use, requiring quite a bit of expertise. Elsewhere, a tool called Keras was developed as a way of making the process of creating a neural network easier out of the box. It sat on top of TensorFlow (or another similar neural network package we're not going to cover here called Theano) and made it so you could make a fully functional neural network in just a few lines of code, emphasizing usability without sacrificing robustness.

Then, even more recently, Keras and TensorFlow integrated, allowing you to use Keras natively with TensorFlow, making modeling even easier. This is a huge part of what has led to the popularity of neural networks as a modeling framework and even Python as a language for data science.

When building a bespoke neural network, we recommend using Keras. That said, to really understand how it works you're going to need to know more about TensorFlow.
