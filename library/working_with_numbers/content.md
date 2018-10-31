---
title: Working with numbers
author: Thinkful
team: grading
time: 240
uuid: 0f63d2f8-f487-4021-a130-11a80c835073
---

As a data scientist, you'll frequently be working with numerical data. In this checkpoint, we'll cover the essentials of working with numbers in Python. This checkpoint ends with a set of drills that you'll work through to practice working with numbers.

## Numbers in Python

In Python there are two primary data types for representing numbers: **integers**, which represent whole numbers like `8`, `42`, and `1337`, and **floats**, or floating point numbers, which represent decimal fractions like `3.5`, `0.2` or `0.6000000000000001`.

Python 3 can represent integers up to any size. Floats, however, [are limited](https://docs.python.org/3.5/tutorial/floatingpoint.html) on how precisely they can be represented. Floats in Python are "double precision" binary floating-point numbers that will represent decimal fractions as precisely as possible with the [52 bits](https://en.wikipedia.org/wiki/Double-precision_floating-point_format#IEEE_754_double-precision_binary_floating-point_format:_binary64). You don't need to know a lot about floating-point errors except that this imprecision makes math a bad idea when you need precise comparisons:

```python
>>> 0.2 + 0.4 == 0.6
False
```

Even if you don't need complete precision floating point errors can quickly compound with one another, so be careful when using floats and know that they have significant limitations.

Let's go ahead and play with some numbers. Read through the code below and print out the examples to see what's going on.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/9d85473fc3"></iframe>


### Arithmetic operators

Ints and floats can be manipulated using the following *arithmetic* operators:

* `+` addition
* `-` subtraction
* `*` multiplication
* `/` "true" division
* `//` "floor" division
* `%` remainder (also known as the "modulo" or "modulus" operator)
* `**` exponentiation

If you haven't yet, take a minute to tinker around with the examples above to see what's going on.

Operations can be grouped, as in Algebra, with parentheses. Python handles order of operations, or [*operator precedence*](https://docs.python.org/3.5/reference/expressions.html#operator-precedence), via *PEMDAS*: parentheses, exponents, multiplication/division, addition/subtraction.

```python
>>> print(6 / 2 * (1 + 2))
9.0
```

### Assignment operators

It's very common to perform arithmetic with numbers assigned to variables and to then want to store the _result_ back in the variable. Consider this example where we completed a new assignment and want to record that in the appropriate variable:

```python
>>> assignments_completed = 9
>>> assignments_completed = assignments_completed + 1
>>> print(assignments_completed)
10
```
One way to accomplish that is to use the syntax above, where we assign a new value to the variable based on a statement including current value of that variable. That might seem weird if you're coming from a math background. For instance, a math formula saying `x = x + 1` is just nonsense. So why does it work in programming? Because the `=` operator here is _assigning a value to a variable_, not _comparing one value to another_, as `=` does in math formulas.

Reassigning values like this is incredibly common, so Python gives us compound assignment operators that will perform an operation and assign the result back to the variable all at once. Here are the assignment operators:

* `+=` add and assign
* `-=` subtract and assign
* `*=` multiply and assign
* `/=` "true" divide and assign
* `//=` "floor" divide and assign
* `%=` modulo and assign
* `**=` exponentiate and assign

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/333e5e4a84"></iframe>

###### Unlike many other languages, Python does _not_ have prefix and postfix operators like <code>++</code> and <code>--</code>. The more "Pythonic" way to increment and decrement numbers is to <a href="">use the <code>+=</code> and <code>-=</code> assignment operators</a>.


### Comparing numbers

Numbers can be compared using the following comparison operators:

* `<` less than
* `<=` less than or equal to
* `>` greater than
* `>=` greater than or equal to
* `==` equal
* `!=` not equal

Here are some examples of comparing numbers:

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/ef28a045d2"></iframe>

The result of a comparison will be a boolean: `True` or `False` depending on how the comparison evaluates. Note that the `==` comparison operator works like the equals sign in math formulas like `2 + 2 = 4`. That math formula is true, and the equivalent Python comparison `2 + 2 == 4` evaluates to `True`.

### Built-in Math Methods

We won't cover it here, but you should know that the Python standard library includes a robust `math` module that will give you common functions like `math.floor()` and `math.sqrt()` and constants like `math.pi` and `math.e`. You can read more in the [math module docs](https://docs.python.org/3.5/library/math.html).



## Assignments


To reinforce what you've learned so far in this checkpoint, please work through the set of drills below. For each drill, you'll need to write a function that implements the required behaviors and passes the test cases we've written for it. As in the previous set of drills, we'll be using Codewars, and there are pre-written tests you must make pass.

Sample solutions are provided at the end of bottom of this page. Give yourself up to 20 minutes to complete each of the drills below, and if you're stuck at that point, hit [Slack](https://thinkful.slack.com/messages/data-science/) or have a look at the solutions and discuss any confusing points with your mentor.

Make sure you're logged into Codewars when you're working through these drills. That will make it easier for you and your mentor to refer back to your code.

1. [Rømer temperature](https://www.codewars.com/kata/thinkful-number-drills-romer-temperature)
1. [Pixelart planning](https://www.codewars.com/kata/thinkful-number-drills-pixelart-planning)
1. [Blue and red marbles](https://www.codewars.com/kata/thinkful-number-drills-blue-and-red-marbles)
1. [Congo pizza](https://www.codewars.com/kata/thinkful-number-drills-congo-warehouses)
1. [Quadratic formula](https://www.codewars.com/kata/thinkful-number-drills-quadratic-formula)

Once you've completed each drill, spend a few minutes reading other solutions before moving on and compare other solutions to yours. Keep a particular eye out for different methods people use to solve the same problem you did. At your next session, be sure to spend some time talking about your answers with your mentor.

Limit yourself to 20 minutes per drill _maximum_. If you're still stuck after that time, hit [Slack](https://thinkful.slack.com/messages/data-science/) or seek enlightenment from the example solutions at the bottom of this assignment. Whether or not you're able to complete each drill on your own, be sure to spend some time talking about the drills and answers with your mentor at your next session.


###### Hey friend, we're here to help! Just a reminder that you can always check out the [Q&A sessions](https://www.thinkful.com/open-sessions/qa-sessions/) if you're stuck or have questions in between your 1-1 sessions. Feel free to drop by for a few minutes or the full hour. Happy coding!

## Sample solutions

Once you've completed these drills or spent twenty minutes working on each one, have a look at these [sample solutions](https://gist.github.com/Grae-Drake/3879ea1c160e60b6a727fb3832ab37cc). Compare and contrast your own approach.

