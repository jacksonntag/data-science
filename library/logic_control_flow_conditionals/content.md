---
title: 'Logic, control flow, and conditionals'
author: Thinkful
team: grading
type: graded
time: 240
uuid: 2507432c-741e-47cc-acba-22eb1aac7dc6
---

In this checkpoint, you'll about three related topics: logic, control flow, and conditionals in Python. Together, these tools will allow you to write programs that can behave differently depending on their inputs.

Take parsing strings as an example. You might write a function that extracts a zip code from a string and stores the result somewhere. When your program runs it may run into a situation where you were unable to find a zip code in the string you're parsing. When that happens you want the ability to programmatically say "if such and such is the case, do this, otherwise do that". That's what you'll learn in this lesson.

Here's what we'll cover:

* boolean values `True` and `False`
* logical operators `and` and `or`
* *control flow* — this refers to the tools provided by a programming language to conditionally determine which set of instructions run. We'll cover `if` / `elif` / `else`, and `try` / `except` blocks, which are two forms of control flow in Python.

This checkpoint ends with a set of drills where you can practice these new concepts.

Before digging in, we recommend printing out this [Python-basic cheatsheet](https://docs.google.com/document/d/1DQB4MgzfPYI90e6xqSQnifo0KV0dni9cK-N4wRe9CX0/edit?usp=sharing). Keep it handy as you're learning the basics of python. It contains common commands you'll want to be familiar with.

## Truth in Python

Before discussing logical operators, which compare the truth value of two assertions, we need to understand the way Python evaluates individual assertions as true or false.

To explore how Python thinks about truth and falsity, we're going to use the built in `bool()` function, which is used to convert a value into either `True` or `False`.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/b15fa9d2e9"></iframe>

Anything that represents "something" is true. Anything that represents "nothing" is false:

 * `False`
 * `None`
 * `0`
 * empty string `''`
 * empty list `[]`
 * empty dictionary `{}`

If you're working with anything else, it'll be true. That means that negative numbers, strings of whitespace, and objects (which we'll learn about later) all evaluate to `True`.

## Logical Operators

Logical operators are used to make assertions about two or more statements or values. Let's start with `and` (logical and), which is used to assert whether or not two statements both evaluate to `True`.

```python
>>> True and True
True
>>> True and False
False
>>> False and True
False
```
In the examples above, Python evaluates the expression on each side of the `and` operator. If both expressions evaluate to `True` it returns `True`.

Well, kind of. When the expressions on both sides of `and` evaluate to `True`, the second expression is returned. In the first example above the second expression happens to literally *be* `True`, so that's what you get back.

A similar thing goes on in the background when one of the expressions evaluates to `False`.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/18c51bc01e"></iframe>

Your intuition with `and` statements will get you a long way. But under the hood this is what's going on:

> The expression `x and y` first evaluates `x`. If 'x' is false, `x` is returned. Otherwise, `y` is evaluated and `y` is returned.

The logical `or` operator is the complement to `and`. It tells us whether at least one of the expressions on either side of `or` evaluates to `True`.

```python
>>> True or False
True
>>> False or True
True
>>> True or True
True
>>> False or False
False
```

Just like `and` expressions, `or` expressions actually return one of the expressions on either side of `or`:

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/31c09c1378"></iframe>

Let's drill down on `or`. Let's imagine we have the expression `x or y` in Python. When this code is executed, first `x`'s Boolean value will be evaluated. If `x` is "truthy", `x` will be returned. Otherwise, `y`'s value will be returned (even if `y` evaluates to False).

Finally, we have the logical `not` operator, which evaluates an expression and gives the boolean opposite.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/1570352cf5"></iframe>

Perhaps more intuitively, `not` always returns a boolean `True` or `False`.


## Assigning default values with logical OR

Why all this complication? Wouldn't it be simpler if `and` and `or` simply returned a boolean?

Consider the following function:

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/830cff0428"></iframe>

In the first line of the function body, we reassign the value of `person` using an `or` operator. If the function is called with a value like `Guido` which evaluates to `True`, then `person` gets the same value again. However, if the function is called with a value like empty string `''` or `None` which evaluates to `False`, then the default value `'world'` is assigned instead.

## Control flow

Control flow dictates how programs execute different sets of instructions based on differing conditions. You might have one branch of code that executes if a condition is true, and another branch that executes if the condition is false. That's control flow, and it's a powerful tool.

We're going to discuss two ways of achieving control flow: conditional statements (`if`, `else`, `elif`) and exception handling (`try` and `except` statements).

### Conditional statements: `if`, `elif`, `else`

Python gives us three keywords for working with conditionality: `if`, `else`, and `elif`. Let's start with an example of [`if`](https://docs.python.org/3.5/reference/compound_stmts.html#if):

```python
def greet_admin(user):
    if user == "Guido":
        return "Welcome, Guido."
```

To use an `if` statement, you begin with `if` followed by an expression (`user == "Guido"` above) and ended by a colon `:`. Below that you indent a block of code to be executed if the condition evaluates to `True`.

The same syntax is used for `elif` (short for "else if") with the additional requirement that `elif` statements must follow an `if` statement. You can use as many `elif` statements as you like.

```python
def greet_admin(user):
    if user == "Guido":
        return "Welcome, Guido."
    elif user == "Bethany":
        return "Welcome, Bethany."
    elif user == "Alex":
        return "Welcome, Alex."
```

The catch-all `else` statement can follow `if` and `elif` statements to end a conditional statement. To use an `else` statement you just use `else:` and begin with your indented code block below. The `else` clause is a catch-all, so you don't include a condition to test. Here's the full conditional statement we've been building.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/82bdbc917d"></iframe>

### Exception handling: `try` and `except`

Python gives us `try` and `except` statements for dealing with conditional logic in the case of *exceptions*. These language constructs allow us to specify a block of code to be tried (the `try` statement). If that block does not succeed, the code in the `except` block runs.

You've probably seen exceptions. Maybe a lot of them if you've tinkered around much :)

Here's one:

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/7cddc2b823"></iframe>

In this example the function is expecting a number to be passed in. When it tries modulo division on a string when evaluating `"Chaos Monkey" % 2 == 0` the program raises an exception, or error. Specifically, a `TypeError`. We don't have anything here to "*handle*" the exception, so our program halts and prints out a *stack trace* (or *traceback*) with information about what went wrong.

Using a `try`, `except` statement instead of an `if` statement lets us "try" executing code that might raise an exception and run code to "*handle*" the exception if it does occur.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/6ca3af577f"></iframe>

Try / except statements give the added benefit of letting your program continue to run. While unhandled exceptions halt your program with a traceback, handling an exception allows your program to gracefully continue along even when you raise an exception and conditionally run code when an exception does occur.


## Assignments

To complete the following drills, you'll need to draw on what you just learned about conditional logic and control flow. For each drill, you'll need to write a function that implements the required behaviors. As in the previous sets of drills, we'll be using Codewars, and there are pre-written tests you must make pass to complete the challenge.

Sample solutions are provided at the end of this assignment. Give yourself up to 20 minutes to complete each of the drills below, and if you're stuck at that point, hit [Slack](https://thinkful.slack.com/messages/data-science/) or have a look at the solutions and discuss any confusing points with your mentor. These drills are intentionally challenging, so don't worry if you struggle with them.

As in the earlier drills, make sure you're logged into Codewars when you're working through these drills. That will make it easier for you and your mentor to refer back to your code.

1. [Traffic light](https://www.codewars.com/kata/thinkful-logic-drills-traffic-light)
1. [Umbrella decider](https://www.codewars.com/kata/thinkful-logic-drills-umbrella-decider)
1. [Graceful addition](https://www.codewars.com/kata/thinkful-logic-drills-graceful-addition)
1. [Red and bumpy](https://www.codewars.com/kata/thinkful-logic-drills-red-and-bumpy)
1. [Hacking p-hackers](https://www.codewars.com/kata/thinkful-logic-drills-hacking-p-hackers)

Once you've completed each drill spend a few minutes reading other solutions before moving on and compare other solutions to yours. Keep a particular eye out for different methods people use to solve the same problem you did. At your next session, be sure to spend some time talking about your answers with your mentor.

Limit yourself to 20 minutes per drill _maximum_. If you're still stuck after that time, hit [Slack](https://thinkful.slack.com/messages/data-science/) or seek enlightenment from the example solutions at the bottom of this assignment. Whether or not you're able to complete each drill on your own, be sure to spend some time talking about the drills and answers with your mentor at your next session.


###### Hey friend, we're here to help! Just a reminder that you can always check out the [Q&A sessions](https://www.thinkful.com/open-sessions/qa-sessions/) if you're stuck or have questions in between your 1-1 sessions. Feel free to drop by for a few minutes or the full hour. Happy coding!

### Sample solutions

Once you've completed these drills or spent twenty minutes working on each one, have a look at these [sample solutions](https://gist.github.com/Grae-Drake/980359db35ed3fd2e5145d83ed564cc3). Compare and contrast your own approach.
