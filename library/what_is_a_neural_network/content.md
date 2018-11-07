---
title: What is a neural network?
author: Thinkful
team: grading
time: 30
uuid: 210c6cbd-419d-4898-bd42-c751dd41ab77
---

Before we do anything more we need to talk. How's it going? You all right? Hopefully things are hard but not, you know, too hard. The sweet spot. Going on a tough hike but not climbing Everest. Maybe you've even seen a few of the signposts that say "Everest, this way" and wandered down those paths for a bit to see what was there. It's fun to live on the edge every now and again. But we haven't strayed far down any of those paths or pushed to too great a height too quickly.

The point is, you shouldn't need oxygen.

But now we're on to neural networks and, well, the air here can get a little thin.

So first a few disclaimers.

## Disclaimers

 * We are going to stick to classical neural networks, occasionally giving hints towards more current, but less used, techniques.
 * The math here is going to be very hand wavy. For most of you it's better that way. If you want the background math we will link to it when we can.
 * Neural networks is an evolving field. If you really love this you should consider getting a PhD in it or at least keeping up with the latest papers from the field and industry.
 * Most data science jobs come nowhere near pushing the bounds of neural networks. If you want to do that, there is a smaller list of places you'll want to apply, and again, a PhD might be necessary for accessing those teams.
 * Some of the _new_ new here is still controversial. Particularly some of the people who are more classical statisticians have issues with neural networks and deep learning, which are a black box and initially it wasn't even really understood why they worked so well in some circumstances. The tide seems to be moving against this perspective, but it is definitely out there.
 * If you want more [this book](http://www.deeplearningbook.org/) is fantastic.

Ok, now we can actually talk about what a neural network is. To do that, we have to talk about the brain.


## Your brain, neural networks, and you

As a human being, you have a brain. And quite a nice one by the looks of it. Well done for making it this far in the course.

Your brain, and your whole nervous system, is made up of neurons and axons. Bear with us on this as some of the biology here will be oversimplified, but these simplifications are perpetuated in the machine learning algorithms we're actually talking about, so they are good to know. 

_Neurons_ can be thought of as the information processors of the brain. They react to signals and create responses. _Axons_ connect neurons to each other. A human brain is made up of billions of neurons linked to each other through a complex web of axons. Information passes through several neurons in response to input or stimulus.

This is the basis of neural networks, the machine learning algorithm. Sometimes these are referred to as "artificial neural networks" so as to differentiate them from the biological variety. Sometimes that differentiation is noted because one is a computer program and the other is a vital organ.


## Artificial neural networks

To explain what an artificial neural network is, let's return to the perceptron.

![single preceptron diagram](perceptron_single.jpeg)

The perceptron model takes in some data and generates a response. Now, previously we mentioned that this is usually a poorly performing model. We've dealt with this problem in the past using ensemble techniques like bagging which gave us random forests. Let's keep that concept of ensemble modeling and have many perceptrons in our model.

![single-layered model](single_layer.jpeg)

Now we're getting closer to a neural network. But let's also recall another ensemble concept: boosting. That's when we take the output from one model and use it as the input for another. Let's use boosting to feed the results from one part of our model into the next part.

![two-layerd model](two_layer.jpeg)

Now that is a serious neural network. A few things to note before we move on and start seeing how to actually implement these models.

Firstly, the columns of perceptrons are called _layers_. Neural networks have layers much like certain pastries, aromatic bulbs, or [green monsters](https://www.youtube.com/watch?v=_bMcXVe8zIs). They can be single layer or multi layered. The first layer is called the _visible layer_.

Any layers after that first layer are called _hidden layers_. These are features built on features. They are called hidden because you're not directly observing their inputs or outputs. They serve as one way of getting around linearity of the initial perceptron boundary. We now have a function of a function, giving greater detail and subtlety to our model.

Now, this model has many many perceptrons, so how are the perceptrons different from one another? Surely we're not just doing the same thing again and again and again, right? To answer that, recall the initial perceptron. Each variable input into the model was given a weight. Here our different perceptrons give different variables different sets of weights. When done at a mass scale (it's not uncommon for a layer to be hundreds or thousands of perceptrons wide) they combine to overcome the initial assumption of linearity, allowing for a model where different combinations of variables have hugely different effects. This ultimately generates a very powerful model.

All of the networks we've shown here are what are called "fully connected". Every perceptron in one layer links to every perceptron in the following layer. You can weight your perceptrons so that they are not fully connected or evenly balanced in their connections.

That second image, the one with a single layer of perceptrons, is actually a simple, single layer neural network. Many-layered networks begin to enter into the realm of _deep learning_.
Also of note is that direction was removed from our final image. The way the layers feed back into each other ends up being a key differentiator in different styles of neural network, so data does not always flow in one direction.

We'll cover all of this in more detail as we get into implementations, but you should now have a conceptual understanding of what a neural network is going to look like. Let's build one!

