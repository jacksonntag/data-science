---
title: Other terms in neural networks
time: 60
---

Before we move on there are a few other terms we need to introduce, just so you're familiar with the 'lingo' the 'kids' are using these days.


## Recursive neural networks

So far when we've talked about neural networks, we've only really referred to them in a feedforward context. _Feedforward_ means there is a clear directionality or flow to the network. Things have started at the beginning, moved in one direction, and proceed to the end. That doesn't have to be the case, though.

Data can run through nodes or neurons more than once. These kinds of networks are called _recursive neural networks_. RNN can be extremely useful for drawing out more complex relationships.


## Convolutional neural networks

If you start working with neural networks, you'll also probably hear about convolutional neural networks. So far we've talked about these neurons linking together in a grid-like structure. If you've read through the additional texts then you know that the grid-like structure can be represented using matrices.

Typically the relationship between layers is (relatively) simple matrix multiplication. However the link can involve another level of complexity by linking those matrices via linear equations, called _convolutions_. Now, these linear transformations are specialized and can have huge effects on the network that you create, but to get into the way we decide these you need much deeper understanding of linear algebra and neural networks than is within the scope of this course.


## Deep learning

Another buzzword running around neural networks and unsupervised learning is _deep learning_. It sounds terribly exciting and if you look at a lot of the literature around data science it could seem like deep learning is the magical solution to everything.

But deep learning isn't magical. In fact, you already know what deep learning is. It's just a neural network with _several hidden layers_. There's no explicit cutoff to when something has enough layers to qualify as "deep" learning. A big downside of deep learning is that the additional complexity can add to runtime and make the model even more of a black box and more difficult to understand what's going on inside.


## Reinforcement learning

Lastly, we should give a quick mention to reinforcement learning. Reinforcement learning is occasionally grouped within supervised learning but more and more it's becoming its own discipline.

_Reinforcement learning_ is an incredibly useful and exciting form of data science, where a model gets feedback from its environment or system. The model tries potential actions at random, and then sees what kind of feedback it receives. In the end it learns a way to operate through a series of events that generates the most positive feedback.

This kind of learning is used for anything from automatically playing a video game (walking into red shells = bad) to learning how to drive a car (crashing into walls = bad). It is a fascinating field and many of the underlying tools are covered in this lesson and this unit as a whole. However, in general it requires a different kind of data than is readily available and a more significant engineering background in order to properly link that feedback loop up than the scope of this course allows.


