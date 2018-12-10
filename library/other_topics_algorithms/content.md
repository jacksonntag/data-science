---
title: Algorithms and data structures
author: Thinkful
team: grading
time: 60
uuid: 3f6099cc-5c2d-418e-9f9e-610841cf5e64
---

## Basic Data Structures

As we've said before, there are plenty of times where we've used an algorithm or data structure in this course. In fact, it's been the vast majority of the course thus far. We've simply taken them for granted, assuming someone else has optimized the algorithm or forcing us to use the right kind of data structure for the job.

So why is it worth spending the time on the specifics?

Simply put, we won't always be able to use someone else's framework to solve our problems. Further more, some situations may also need to be highly optimized, and we can't rely on others to do that for us. When we're dealing with a static dataset of a few hundred thousand rows, we may care about efficiency, but often the stakes aren't that high. The difference can often be between waiting for half a second and two seconds, which isn't a difference worth spending hours trying to optimize.

However, what if we're trying to run our model in production? And what if our model is handling hundreds of events per second? How do we store those events? How do we handle new entries and solved entries? Now we want to optimize that process as far as we can. A difference of milliseconds can hugely affect how well this process scales.

The process we're talking about can be as simple as managing a queue, which is a classic example that will allow us to introduce both simple data structures and the basics of algorithms. Many things related to data science involve managing a queue, from support tickets to data requests and more. For our example however, let's just think of a queue.

![Waiting for doughnuts](Line_in_front_of_Voodoo_Doughnut.jpg)

For our purposes our queue is a series of arrivals that need to be remembered, with each entry needing some process to be done to it. We have to manage a queue because sometimes our arrivals might come more quickly than we can process them and we don't want new arrivals to be lost if we're busy. In other words we'll have two separate stages, the _queue_ (the topic here) and the _processing_ (which we'll address in the next lesson).

What are the ways we could handle this?

## The List

The first and likely most familiar data structure for handling this kind of data would be a list. Now, a list in formal computer science is defined slightly differently than the particular _implementation_ in Python. We want to think about data structures in the abstract, not how any particular language implements them. Once we've got a good handle on the abstract data structures we can dive into language specifics.

Now, back to the list.

In its most essential terms, a list is an __ordered sequence of items with an incrementing index__. What does that actually mean? Well, it's a lot like the Numpy arrays and Python lists we've worked with so frequently in this course. Our entries each have an index (starting at 0) and that index increases for each item in the sequence.

There are several conveniences to this. Firstly we can call any element of the list simply by knowing its index. We want the 3rd element, we just have to look for index 2. We can also easily add new items to the list without changing anything in the pre-existing list. We just need to add the new item at the next index.

However, that indexing also gives us some inconveniences that a queue does a particularly good job of revealing.

Let's say we wanted to run a first in, first out queue (also called a FIFO queue). This means we want to handle the person who's been around the longest first. They should be at the head of our list, in position 0. So let's say we want to remove them from the list. What happens to the list now? Do you see the problem?

Well, if we are using a list we need to keep our first entry indexed with 0. So when we remove an element we have to go through the remaining entries and decrease their index values accordingly. This may not be that much of a problem if the list is small, but again when we're looking for real efficiency that is going to take some time that we don't want to sacrifice. Imagine you removed the first book on this shelf:

![Books!](books.png)

To keep your indexes straight you'd have to shift every book over by one. That's a lot of work.

As for implementation of lists you can actually use, Python has you covered. Python lists and Numpy arrays both work this way, so you'll rarely implement your own version lists from scratch. That's not the case with some data structures we'll cover later.

## Efficiency & fundamental steps

We've been talking about efficiency and how it can be important in some contexts, so let's formalize our definitions of efficiency and inefficiency. Earlier in the course [we introduced Big O notation](https://courses.thinkful.com/data-201v1/assignment/2.2.2).  Big O is a way of quantifying the efficiency of a process in terms of the size of the data structure you're dealing with as input.

Think about a process and breaking it into the smallest "steps" you can imagine. In programming, these _steps_ (or "fundamental instructions" in computer science lingo) are things like assigning a value to a variable, reading a value, or comparing two values for equality. When we think about efficiency, we try to think about how many steps it would take for us to complete a process and how that number changes as the size of our input data increases. Remember, Big O is about asymptotic efficiency, which incorporates this approaching of a limit.

Can you see what the worst case efficiency of removing an item from a list is?

Our worst case scenario is typified by our FIFO queue. We'd have to remove that first item and then adjust every following entry's index. This would be called O(n) where n represents the length of our list. The longer the list, the more time it takes, and that time scales linearly.

## Linked List

Now let's think about how we could get a bit more efficient with operations like that. This leads us to a structure called a linked list.

In a _linked list_, we maintain order of our items but do not have an index. Instead, each entry is linked to the next item. Linked lists can be either singly or a doubly linked, depending on whether the links only point forward or whether they also point backwards.

What's the advantage of getting rid of indexes and pointing to the next item instead?

One advantage is deletion, which is O(n) for lists but only O(1) for linked lists. This is because we only update the pointer (or pointers in a doubly linked list) that was pointing to the removed item rather updating the index of every item that follows.

But what about accessing? Accessing is the process of going to find a specific value. Here linked lists are at a disadvantage to lists, where accessing values is O(1). For linked lists the efficiency is O(n) because we always have to start at the first item and move through the chain until we get to where we want. There is no fast way for us to go to a specific place since there is no index for us to reference.

Python doesn't include an implementation of a linked list, so to use it you have to write it yourself. This is typically done using a `Node` class that stores the value of an item plus a pointer to the next node (and the previous node in a doubly linked list).

Here's an implementation of linked lists in Python. This includes methods for common operations like appending, removing, and inserting nodes. Review the code and the comments thoroughly before moving on.

<iframe src="https://trinket.io/embed/python3/17e1d1c231" width="100%" height="600" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>


## Queue

There's a version of the linked list that is a bit more specialized and it's designed to solve exactly the queueing problem we started with. Unsurprisingly, it's called a _queue_.

A queue is a single linked list, but with the special feature that items only come in at one end and leave at the other. This is exactly what we described as our FIFO queue. Then we think of entering the queue as "enqueing", where items get linked to the last element of the list. We can then only remove from the front of the line via a "dequeing" process.

This is an optimal data structure for managing our queue because it lets us do exactly what we'd want to in O(1) efficiency.

Its drawbacks are in accessing and searching. To get an element from another part of the queue or just search the queue to see if an element is present, we'd fall into O(n) efficiency. Not the end of the world, but this just illustrates that queues aren't perfect for everything.

## Stack

Lastly, you can make a stack. This could also be a LIFO queue. In this case it's a linked list where items are only added or removed from one end. This means to access an element further down the queue we'd have to first remove all preceding elements. Not ideal for many circumstances, but it does have its uses.

![Full stack developer amirite?](stack.png)

As we said at the beginning, we're just scratching the surface of this topic. Luckily there are plenty of other resources on algorithms and data structures in Python. Some we recommend if you want to dig deeper are [Interactive Python](http://interactivepython.org/runestone/static/pythonds/index.html) and [Python School](https://pythonschool.net/category/data-structures-algorithms.html), plus [this tutorial on complexity](http://discrete.gr/complexity/) if you need a refresher on Big O notation. Keep in mind as you review these other sources and scour the internet for other implementations that these things can be done in many different ways. There is no single right way or right choice and don't be surprised to see variations.