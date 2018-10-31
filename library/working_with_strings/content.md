---
title: Working with strings
author: Thinkful
team: grading
time: 240
uuid: 32509423-b6b8-4009-8336-06f1fc9ab9a5
---

As a programmer you'll frequently work with strings. Here are some common scenarios where you need to understand strings:

* dealing with any textual data
* handling and presenting output from your program
* files like CSVs are basically one large string


In this checkpoint, we'll cover the essentials of working with strings in Python. This checkpoint ends with a set of drills that you'll work through to practice working with strings.


## What is a string?

```python
string_example = 'This is a string!'
```

A string is a *sequence of characters*. In Python, we can assign string values to variables by using either single or double quotes around our sequence of characters.

```python
>>> spam = "Spam!"
>>> eggs = 'Eggs!'
>>> print(spam)
'Spam!'
>>> print(eggs)
'Eggs!'
```

Either single or double quotes are fine. The key is that the outermost quote delimiters must both be either single or double.

You can also use triple quotes `'''` to create big multi-line strings:
```python
book_of_armaments = '''
And the Lord spake, saying, "First shalt thou take out the Holy Pin.
Then shalt thou count to three, no more, no less.
Three shall be the number thou shalt count, and the number of the counting shall be three.
Four shalt thou not count, neither count thou two, excepting that thou then proceed to three.
Five is right out.
'''
```

Strings are used to represent text. Python 3 handles strings much better than Python 2, which is one of Python 3's great strengths. Python should be able to handle just about any Unicode that you throw at it, so strings like `"passé"` and `"schöne"` and "`ねこ`" are all fair game.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/ff4401158d"></iframe>

Once you've read the examples above take a few minutes to change the values of the strings you define, define some brand new strings, and `print()` out the results.

## Special Characters and Escaping

Some characters can be tricky to use. Let's say you want to use the `"` character inside of a string. Maybe you want to use double quotes to represent a quotation. One way to do that is to wrap your string in single quotes `'`, but what if that isn't an option? Or what if your string _also_ includes an apostrophe?

This is a case where we need to use a `\` backslash in order to *escape* a character:

```python
line = "He said, \"Sure, let's go!\"";
```

In other contexts, the backslash is used to indicate special characters, such as a line break (`\n`) or a tab (`\t`) character. For instance, `'name:\tJohn'` would give us a string with "name:" and "John" separated by a tab.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/9a92d44a6d"></iframe>


## Concatenating and Repeating Strings 

Python lets us use the `+` operator to *concatenate* — which just means "connect" — two strings into a bigger one.

You can also use the `*` operator to *repeat* a string.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/ab286d0ff5"></iframe>

## Indexes and Slicing

Each character of a string has an index, starting at `0` for the first character. You can access each character in a string by index using bracket notation.

```python
>>> 'Hello'[0]
'H'
>>> 'Hello'[4]
'o'
```
You can also access larger chunks of a string using *slicing*. While using a single index will give you a single character, using two indexes separated by a colon `:` will give you a substring:
```python
>>>'Monty Python'[0:5]
'Monty'
>>> 'Monty Python'[6:8]
'Py'
```
The character at the start index is always included in the substring you get back, and the character at the end index is always _excluded_.

When slicing strings you can omit one of the indexes and Python will assume you want to start from the beginning or go all the way to the end, depending on which index you omit.
```python
>>> 'Monty Python'[:5]
"Monty"
>>> 'Monty Python'[6:]
"Python"
```
You can also use negative numbers as indexes. When using negative numbers you start counting from the end, beginning with `-1` as the last character in a string.
```python
>>>'Monty Python'[-1]
'n'
>>> 'Monty Python'[-3]
'h'
```


## Comparing Strings

You can use the `==` operator to compare two strings to see if they're identical.

```python
>>> food = 'eggs';
>>> breakfast = 'eggs';
>>> lunch = 'spam';

>>> food == breakfast
True
>>> breakfast == lunch
False
```

###### You might think the comparison operator `==` looks a lot like the assignment operator `=`. In fact, using the assignment operator `=` (which _looks_ like an equals sign in math) when you meant to use the comparison operator `==` (which _acts_ much more like an equals sign in math) is one of the most common mistakes beginning Python programmers make.

## String methods

All strings in Python share a number of [built-in methods](https://docs.python.org/3.5/library/stdtypes.html#string-methods). Methods are called by following the string with a `.` , then the name of the method, and then parentheses `(` `)` surrounding arguments, if any, that you're passing in to the method. Here are just a few examples of built-in string methods:

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/01a8f9b42f"></iframe>

Did each of those examples print like you expected? The next assignment is a series of drills using the topics we've covered so far, so take a minute now to play around with the methods above.

## Assignments

To reinforce what you've learned so far in this checkpoint, please work through the set of drills below. For each drill, you'll need to write a function that implements the required behaviors and passes the test cases we've written for it.

These drills are presented on Codewars. If you don't yet have one, go to Codewars and [create an account](http://www.codewars.com/join). To sign up you'll need to solve a small challenge. Choose Python and keep the `return` keyword in mind for the challenge. We recommend adding "Thinkful" as your clan so you can more easily compare your work to other students.

Know that each drill has a set of pre-written *tests*. These tests tell the program what to expect from your code. In order to complete each drill you'll need to write code that makes all of the tests pass. Later you'll learn how to write tests for your own code. For now your job is to write code that will make the pre-written ones pass.

1. [Hello world](https://www.codewars.com/kata/thinkful-string-drills-hello-world/python)
1. [Quotable](https://www.codewars.com/kata/thinkful-string-drills-quotable/)
1. [Repeater](https://www.codewars.com/kata/thinkful-string-drills-repeater)
1. [Repeater, level 2](https://www.codewars.com/kata/thinkful-string-drills-repeater-level-2/python)
1. [Jedi name](https://www.codewars.com/kata/thinkful-string-drills-jedi-name)
1. [Areacode extractor](https://www.codewars.com/kata/thinkful-string-drills-areacode-extractor)
1. [Poem formatter](https://www.codewars.com/kata/thinkful-string-drills-poem-formatter)

Once you've completed a drill, or "*kata*" as they're called on Codewars, you'll be able to see the solutions that other people have submitted. One of the best ways to become a better programmer is to read code other people have written, so every time you complete a drill spend a few minutes reading other solutions before moving on and compare them to the solution you wrote. At your next session, be sure to spend some time talking about your answers with your mentor.

Limit yourself to 20 minutes per drill _maximum_. If you're still stuck after that time, hit [Slack](https://thinkful.slack.com/messages/data-science/) or seek enlightenment from the example solutions at the bottom of this assignment. Whether or not you're able to complete each drill on your own, be sure to spend some time talking about the drills and answers with your mentor at your next session.


###### Hey friend, we're here to help! Just a reminder that you can always check out the [Q&A sessions](https://www.thinkful.com/open-sessions/qa-sessions/) if you're stuck or have questions in between your 1-1 sessions. Feel free to drop by for a few minutes or the full hour. Happy coding!

## Sample solutions

Once you've completed these drills or spent twenty minutes working on each one, have a look at these [sample solutions](https://gist.github.com/Grae-Drake/c4fe8527edf0217712dff37b0cf09a21). Compare and contrast your own approach.

As you read more and more code written by other people you'll come to appreciate how many different ways there are to solve even simple problems. There probably isn't a "right" way to solve most problems, but there are different ways in which code can be better or worse: different **tradeoffs** you can choose between. Code can be easier to read or more obscure, maintainable or fragile, performant or slow, Pythonic or written like Java. Often times there are trade offs between these qualities and doing well on one means doing poorly on another. It's foolish to strive for perfection. Instead, your goal should be to understand the tradeoffs you're making and be deliberate about the choices you make. This is a difficult skill, and one you will continue to develop throughout your entire career.


