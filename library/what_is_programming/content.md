---
title: What is programming
author: Thinkful
team: grading
time: 30
uuid: 0854019d-cdb5-4e96-accd-2a478547350f
---

A *program*, in simplest terms, is a set of instructions for a computer to carry out. In the context of data science, you might write a program to collect data from the web, or to systematically reformat or clean your data once you've collected it, or to process your cleaned data and display an interesting visualization of your user networks. There's literally an infinite number of programs you could write.

We write programs to solve a specific problem or provide a specific experience. The skill of programming therefore has two steps: first, programming is finding solutions to problems; second, programming is implementing those solutions in a particular programming language such that your computer can understand and execute your solution.

In this checkpoint, we're going to explore this idea of programming as problem-solving with a brief example: computing the digits of the Fibonacci Sequence and displaying them to an end user. We'll see how we can move from stating a problem in plain language to solving and implementing it using Python.

The purpose of this example is not to get you up to speed on Python, but instead to allow us to talk about programming — how problems can be broken down into distinct, elegant functions that specialize in doing a single thing and doing it well.

## The Fibonacci series

The [Fibonacci sequence](https://en.wikipedia.org/wiki/Fibonacci_number) describes a series of numbers in which each number in the list is the sum of the previous two (with the exception of the first two numbers in the list, 0 and 1).

The first six numbers in the Fibonacci sequence are: 0, 1, 1, 2, 3, 5.

The *algorithm* — or set of instructions — to produce the Fibonacci numbers is as follows:

1. Define an integer value, `n`. `n` determines the length of the list of Fibonacci numbers output by the algorithm.
2. Set the first two items in the resulting list to 0 and 1 respectively.
3. For a remaining `n - 2` times (`n - 2` because the first two slots in the Fibonacci sequence are taken by 0 and 1 - we're assuming `n > 2`), compute the next item in the list by adding the previous two.
4. When the list's length is equal to `n`, we're done.

This sequence of numbers has applications in mathematics and biology, but we're interested in it now because it's a known algorithm that we can implement. When you're programming, sometimes you must invent algorithms, and other times you implement existing ones. Most of the time, you're doing a bit of both.

## Showing Users the Fibonacci Numbers

Suppose we want to create a simple interface that visually displays the Fibonacci sequence to users. The user should be able to tell us how long of a list of Fibonacci numbers to display. After they input their answer, the interface should compute and display a series of the correct length.

This user experience can be broken down into three distinct moments:

* getting the number of results to compute from the user
* computing an n-length list of Fibonacci numbers
* displaying that list of numbers

These seem like three bits of distinct functionality, so we have a good starting point for defining and implementing three distinct functions in a Python program.


## Implementing a Fibonacci program

Below, we've implemented a Fibonacci program similar to what we just described. The key difference is that we've simplified the interface slightly. Instead of allowing the user to set the list length, we manually set its length to 20.

###### In the example below and frequently throughout this course we're going to use an embedded Python REPL ("Read Evaluate Print Loop"). You can tinker with these examples by editing and running the new code directly in your browser. Later, we'll walk you through setting up Python and your local development environment.

Spend a minute and read the Python code below. Read through the code comments for commentary on how the code works. Don't worry about trying to learn the syntax of Python just yet.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/0e0f16ed01"></iframe>

The architecture of this program (three distinct functions -- `get_fib_list_length`, `generate_fib`, and `display_fibs` — which are together called by the `main` function) reflects the way we broke down our problem in plain language before beginning to code ("We need a way to determine how long the list should be", "We need a way to generate a list of Fibonacci numbers up to a certain length", "We need a way to display the list to a user").

Programmers by definition must master one or more programming languages, but this ability to move from high level language, to a clear set of instructions, to implementing the instructions using clean code — _that_ is the key skill of the programmer.

Your goal in the remainder of this course is both to become literate with Python **and** to develop this more difficult problem solving skill common to good programmers.