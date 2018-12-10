---
title: Let's talk Keras
author: Thinkful
team: grading
time: 45
---

So we said in the beginning that we'd use Keras to build Neural Networks, but so far we've been all about the TensorFlow. That changes now. But before we can start using Keras, we need to discuss how it's different from TensorFlow.

Keras is a much more user friendly system than TensorFlow.  It was designed to work quickly while maintaining as much adaptability as possible. Of course sacrifices are still made, and it is nowhere near as flexible as TensorFlow. 

Hopefully through the past two lessons you have seen the very granular controls that TensorFlow gives you for setting up a session and creating a model. Keras is not that kind of program. Made specifically for neural networks, Keras aims to give maximum flexibility while maintaining a relatively easy frame of use. As such it emphasizes modularity of customizability. How does it do that? While, it all comes down to how Keras thinks about structures. Instead of Nodes and Variables and the like, Keras thinks in terms of Models and Layers.

# Keras has Layers...

The simplest level of structure in Keras is the layer. These are like the layers we discussed in the previous neural networks section, a set of nodes or perceptrons that connect in some form to both the preceding and following layers.

There are many different kinds of layers in Keras. Perhaps the most common of these layer types is `Dense`. Dense layers are also called fully connected layers, where each node connects to each node in the following layer.

There is a (lot more to layers)[https://keras.io/layers/about-keras-layers/] than just Dense. You have convolutional layers or recurrent layers or many other kinds that we haven't even discussed. The documentation here is really strong, and as you expand the kinds of networks you build, we recommend referring back to it. To explain every possible type of layer here would be work worth of a dissertation, if not several. We’d generally advise you to stick to structures you read about elsewhere rather than attempting to innovate in this space until you’ve spent a lot more time working on these kinds of models.

# Model Types

Models in Keras come in two varieties: Sequential and Complex.

Sequential is the simpler of the two to implement, and implies a basic stack of layers with a linear progression. The more complex models (made through the Keras API) have any kind of graphical structure you could imagine.

So how do you make a model? You add layers.

```
from keras.models import Sequential

model = Sequential()

from keras.layers import Dense, Activation

model.add(Dense(units=100, input_dim=100))
model.add(Activation('relu'))
model.add(Dense(units=10))
model.add(Activation('softmax'))

```

This sets up a sequential model, and then adds two layers with two different activation functions. These layers are fully connected, or ‘dense’. Also note that the first layer specifies units (which is the width of the layer) and the input dimension (which is necessary for the first layer in order to specify the number of input variables).

Also, your last layer has a number of units that is the number of outputs you want. So ten outputs would be for a ten class classifier, with a softmax function to pick which category (again, there are more functions to choose from, this is just one of the most common for classification problems).

# Compile and Fit

Once you've established the model, you have to compile it and then fit it.

To compile the model specify two things: loss and optimizer. The loss function explains what we'd want to minimize, as before, and Keras has several kinds of loss functions built in under `keras.losses`. You can find the one that would be most appropriate to your given problem.

The optimizer is something we addressed in the previous lesson with the implementation of gradient descent, the primary optimizer we've covered thus far, though under `keras.optimizers` there are several other options.

These are the key components for working with Keras: now is the time to build something with them.