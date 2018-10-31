---
time: 30
title: Algorithms basics
author: Thinkful
team: grading
uuid: 686422f5-e295-4687-8629-41e1303c2f30
---

As we get into the modeling sections of this course, it’s important to stop and introduce algorithms. We’ll talk about algorithms in detail in their own section later in the course, but we’ll introduce some of the basic concepts here that will help you to understand the models we cover and how they actually work.

If you were to ask Python to run a model, it doesn’t know what to do. If you were to just type into your environment "Model my data, please" your computer wouldn’t know what to do. It would come back with something to the effect of "I don’t know what any of that means", like maybe `-bash: Model: command not found`. Instead we (or someone who builds a package like scikit-learn) have to give Python a specific set of instructions to generate the model we want or find the best solution as we define it. Those instructions are an _algorithm_.


## What is an algorithm?

Algorithms are everywhere in data science. They are how we’ll sort lists. They are how we run tests. They are how we will build our models.

An _algorithm_ is a set of instructions for a computer. Common non-computing examples include a set of driving directions ("turn north on highway 101, then take the second left after the old oak tree") or a recipe (mix the eggs and butter, then add to the dry ingredients). Whichever way you choose to describe it, algorithms are how we get to computers to combine simple operations like basic maths or assigning values to variables into behavior capable of solving complex tasks like browsing the internet or predicting the future. We’ll rely on algorithms to build models in this course. Throughout the course we’ll introduce some of the classic algorithms of data science.

Much like directions or a recipe, there are many ways to write an algorithm that can give the same result. However, not all algorithms are created equally. One criteria on which we will judge algorithms is _efficiency_.


## Steps

Before we think about the larger topic of algorithmic efficiency, we must first talk a little more about how algorithms function. To do this we should think about _steps_ or instructions. These are the things that the computer actually has to do when running your code. It can be something simple, like this:

```python
>>> 5 == 4
False
```

This is a n equality comparison of 5 to 4, and it takes the computer one step to check this.

Computers can do many things in a step. You can assign values to a variable, make a comparison between two numbers, change a variable’s value, look up the value of a list element at a specific index, or many more things. If it’s an active task for the computer it’s probably a step. Breaking down code into basic steps is an important exercise in algorithm design because it allows us to see how efficient our code is and make sure it's as efficient as possible.

It can be tempting to think of a line of code as a single step. However, that is not true because not all lines of code behave the same way. For instance:

```python
>>> numbers = [1, 2, 3, 4, 5]
>>>
>>> for i in numbers:
…     print(i > 4)
False
False
False
False
True
```

Here we have a loop that will actually run multiple times. The code inside the loop represents a step that happens for _each element_ of the list `numbers` since the comparison against `4` happens for each element.


## Algorithmic efficiency and complexity

So we’ve gone through some details in how computers actually move through an algorithm and what it means for a computer to actually ‘do a thing’. The question that remains, of course, is why does this matter?

You could probably guess by the fact that we’re devoting a section to this that it matters. It matters a lot to data science in particular because we are often dealing with huge amounts of data. With a single observation a computer can get away with being inefficient and taking a significant number of steps to do something. The more data you have, however, that tolerance for inefficiency goes down. It starts to matter how much work it takes for a computer to work with large scale data.

Different kinds of algorithms scale in different ways.

Our comparative for loop, for example, scales linearly and is said to have _linear complexity_. Every additional element in the dataset, (our list `numbers`), adds an additional step to the algorithm.

However, let’s say we had a more complex loop:

```python
>>> numbers = [1, 2, 3, 4, 5]
>>> 
>>> for i in numbers:
…     for j in numbers:
…         print(i > j)
False
False
False
False
False
False
True
False
[...17 more lines]
```

This algorithm no longer scales linearly. If we have one element in `numbers`, the print statement runs once. However, if we have two elements it runs four times. If we have three elements it runs nine times. Can you see the pattern? It scales according to the square of the length of `numbers`. This algorithm has _quadratic complexity_. 

Though this example may be trivial and not practical code to write, the concept is very much at the core of algorithmic efficiency. Different algorithms see the number of steps they take grow at different rates and in different functional forms.


## Big O Notation
**Big O Notation** is the way to describe this scaling rate. For each particular algorithm you can use big O notation to describe a limiting functional form. As the number of elements in the algorithm’s input grows, this notation shows the lower bound of performance. So something that is O(n) will be at worst n steps. O(n^2) is at worst n^2 steps. It is somewhat similar to a pizza delivery guarantee like 30 minutes or less. For something that is O(n), your algorithm will run in n steps or less.

Recall our first algorithm above with linear complexity. It's described as O(n), where n is the length of the input list. Our second algorithm, the one with nested for loops and quadratic complexity, is O(n^2) where, again, n is the length of the input list.

When thinking about big O, we only care about the things that grow most quickly as the dataset scales. For instance, look at the line `y = 2` in the example below.

```python
>>> y = 2
>>> numbers = [1, 2, 3, 4, 5]
>>> for i in numbers:
…     print(i > y)
False
False
True
True
True
```

That line exists outside of the loop and will always be executed exactly once. The number of steps it represents doesn’t depend on how many items are in n. It's constant, while the steps inside the loop do scale with the size of n.

The key here is that when we use big O notation to refer to an algorithm’s complexity, we’re talking about how efficiently the algorithm scales with additional data. For some datasets we can be ok with relatively inefficient algorithms, but in practice efficiency often matters because it sets an upper bound on the size of the dataset you can reasonably work with. In fact, sometimes you might even manually re-implement algorithms you have access to with libraries like NumPy for efficiency reasons because your use case allows you to trim parts of the algorithm away.

For a deeper dive into algorithms and complexity, see [this optional extension](http://discrete.gr/complexity/). Throughout the course we’ll introduce the algorithms that power some of our favorite models and talk about their complexity. We’ll also cover the topic of algorithms in their own right towards the end of the course.

