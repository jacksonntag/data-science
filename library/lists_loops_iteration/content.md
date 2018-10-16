---
time: 180
name: Lists, loops, and iteration
---


So far, you've learned the basics of working with variables, numbers, strings, functions, logical operators and control flow in Python. In the examples we've, we've been operating on single inputs. So far the functions you've created in the drills have worked on one name or one set of numbers or one weather forecast at a time.

In this checkpoint, we'll learn about collecting a group of data together in a *list* data structure and using *loops* to iterate over the data contained in a list or in another sequence.

As a programmer and a data scientist, you'll work with collections of data all the time. Proficiency with lists and loops is a key step in that direction.

At the end of this checkpoint, you'll work through a set of drills where you'll practice the concepts you learn about.

## Lists

Lists are used to store a collection of data in an ordered sequence. List items can be of different data types.

```python
['Hello', 42, 3.414, True, None]
```

List items can even be other lists, allowing for multidimensional matrices.

```python
[['X', 'O', 'X'], ['O', 'X', '0'], ['X', 'O', 'X']]
```

When you're working with vanilla Python and dealing with a problem that involves collections of things, chances are good you're going to be dealing with lists. These could be collections of email addresses, numeric data, file names, etc.

### Creating lists

To create a list, we use square brackets (`[]`). We separate items in the list with commas. It's customary to follow each comma with a space. Lists can be created with zero or more elements.

```python
>>> empty_list = []
>>> letters = ['a', 'b', 'c', 'd']
```
You can also use `list()` on another iterable such as a string or a range (we'll cover ranges later) to generate lists:

```python
>>> list("Hello")
['H', 'e', 'l', 'l', 'o']
>>> list(range(10))
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Accessing and updating lists

List contents are accessed by *index* using bracket notation; just like strings. You can access an item in a list by asking for the item in a given position.

```python
>>> all_the_things = ['cats', 'dogs', 42, ['pizza', 'beer'], True]
>>> first_item = all_the_things[0]
>>> print("The first thing is '{}'.".format(first_item))
The first thing is 'cats'.
```

Note in this example that we start counting list items at 0, just like we do with strings. This may still seem strange, but that's simply how we count sequences like lists and strings in Python.

Similar syntax is used to update an item at a particular index in a list. Here we set the first element in `all_the_things`:

```python
>>> all_the_things = ['cats', 'dogs', 42, ['pizza', 'beer'], True]
>>> all_the_things[0] = 'bears'
>>> print(all_the_things[0])
bears
```

### Slicing lists

Earlier when we covered strings you saw that you could access multiple characters in a string with *slicing*, using bracket notation and two indices separated by a colon `:`. 

```python
>>> 'Monty Python'[:5]
'Monty'
```
You can use the same slicing syntax to create a slice of a list:

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/d9efed8078"></iframe>

Note that slicing _doesn't affect the original list_. Instead, slicing a list will return a new list representing some or all of the original list.

### The built-in `len()` function

Python has a built-in [`len()`](https://docs.python.org/3.5/library/functions.html#len) function that will tell you how long a list is by returning the number of items in a list.

```python
>>> letters = ['a', 'b', 'c', 'd']
>>> print len(letters)
4
```

## List methods you should know

Lists have [about a dozen methods](https://docs.python.org/3.5/tutorial/datastructures.html#more-on-lists). There are use cases for all of them, but here we want to draw your attention to some of the most commonly used methods.

### `.append()`

The `.append()` method is used to add, or "append", a value to the end of a list. Methods such as `.append()` are called by following the list you want to work with by a dot `.`, then the name of the method, then parentheses `(` `)` containing the argument(s) you want to pass in.

```python
>>> letters = ['a', 'b', 'c', 'd']
>>> letters.append('e')
>>> print(letters)
['a', 'b', 'c', 'd', 'e']

```

### `.insert()`

The `.insert()` method is used to insert a new value at any position in a list, including the beginning, middle, or end. You call it with two arguments: the index you want to insert at and the value you want to insert:

```python
numbers = ['one', 'two', 'four']
numbers.insert(2, 'three')
print(numbers)
['one', 'two', 'three', 'four']
```

### `.pop()`

The `.pop()` method is the opposite of `.append()`: it removes and returns the final item in a list. This is the first list method we've seen that has a return value; `.append()` and `.insert()` modify the underlying list but don't themselves have a return value. No arguments are needed with `.pop()`.

```python
>>> to_do = ["Conquer world", "Install Linux", "Change light bulb"]
>>> current_task = to_do.pop()
>>> print(current_task)
"Change light bulb"
>>> print(to_do)
["Conquer world", "Install Linux"]
```

### `.index()`

The `.index()` method is used to find out the first index number of a matching list item. There is one required argument (the item you want to match), followed by two optional start and stop index arguments in case you want to limit your search to a particular slice of the list. Like `pop()` it returns a value: the index number of the first matching element

```python
>>> fowl = ['duck', 'duck', 'goose', 'duck']
>>> fowl.index('goose')
2
>>> fowl.index('duck')
0
```

### `.sort()`

The `.sort()` method is used to re-order a list. Like `.append()`, `.sort()` has no return value. It directly modifies the list you call it on and _does not_ create and return a new sorted list.

```python
>>> words = ['car', 'boat', 'apple', 'banana']
>>> words.sort()
>>> print(words)
['apple', 'banana', 'boat', 'car']
>>>
>>> ids = [15, 26, 41, 1]
>>> ids.sort()
>>> print(ids)
[1, 15, 26, 41]
```

You can use optional arguments to change the default sorting behavior, but most often `.sort()` is called with zero arguments to automatically compare the elements directly as in the examples above.

Here is an interactive environment with the examples above. Tinker around with these list methods and print things out to test your mental model of how things are working.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/e4041e16a0"></iframe>


## Loops and iteration

In programming, a *loop* is a construct that allows you to repeat a set of instructions a specific number of times, or until a specific condition is true. 

Lists are one example of a *collection* of things, and the data in a list might represent Tweets, emails, statistics, friends, or so on. Loops give us a way to write a set of behavior once and then apply that behavior to each item in these collections or apply it a certain number of times. This is a valuable tool to have in our problem solving kit.

Here, we're going to look at two kinds of loops: `for` loops and `while` loops.

### `for` loops

`for` loops are used to run through a block of instructions a specific number of times. Here's a minimal example that just prints a message each time the loop runs:

```python
>>> names = ["Bethany", "Alex", "Grae"]
>>> for name in names:
>>>     greeting = "Hello " + name
>>>     print(greeting)
Hello Bethany
Hello Alex
Hello Grae
```

As you can see, this code will loop over the list we assign to `names` and repeat the code inside the `for` loop once for each item in the list.

Let's dig into the syntax of this loop. First off you begin with `for`, which signals that you're starting a loop and indicates which kind of loop it is. Then we follow with the variable name we'd like to give to each item in the list. In our example the entire list is called `names` and we're calling each string inside the list `name`. Next use the `in` keyword followed by the collection you're iterating over. We end the line with a colon `:`, which indicates that we're ready to begin our indented block of code that will be executed each time the loop iterates.

###### Using a plural name for a list and the singular of that name in a loop like this is very common. You might have a list of "area_codes" use a for loop that looks like <code>for area_code in area_codes:</code>, or a list of "users" and use a for loop like <code>for user in users:</code>. This style of naming is a useful convention, not a requirement.

Inside the indented code block we can run any code we like. The example above accesses and uses each item we're iterating over, but that doesn't need to be the case.

```python
>>> names = ["Bethany", "Alex", "Grae"]
>>> for name in names:
...     print("There's no place like home.")
There's no place like home.
There's no place like home.
There's no place like home.
```

Lists are one type of sequence that works with `for` loops. What about other sequences like strings or ranges?

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/d9def62747"></iframe>

Use `for` loops whenever there is a block of operations that you want to perform on each value in a set of values, or when you want to perform a specific number of times. You'll find that happens very frequently.

###### If you're coming from another language with a C-like syntax for for loops that requires you to think about the index variable and looks like this: <code>for (i = 0; i < list.length; i++) {}</code> then it might feel weird to iterate without having to think about the index. While the more "Pythonic" solution to most problems usually doesn't require it, you can use the built-in <a href="https://docs.python.org/3.5/library/functions.html#enumerate"<code>enumerate()</code></a> function if you need to see which index you're working on inside the loop.


### `while` loops

[`while` loops](https://docs.python.org/3.5/reference/compound_stmts.html#the-while-statement) are another, less common way to loop. We said that `for` loops execute a block of instructions a specific number of times. `while` loops are useful when you aren't sure how many times you need to loop and will continue to iterate as long as the logical condition you provide is true.

Here's an example that keeps dividing an integer by two as many times as possible:

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/753ea466cb"></iframe>

To write a `while` loop you start with the `while` keyword, followed by an *expression* that evaluates to `True` or `False`. In the example above that expression is `n % 2 == 0`. If the condition evaluates to `True`, the loop will run; if not, it won't and execution of the program will continue on below.

Conceptually, `while` loops are meant to be used where the looped behavior does not have a known number of iterations, but instead a known logical condition where it should terminate. One common use is to gather and validate user input.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/3eb52e1ac0"></iframe>

There's another common, but potentially confusing, use of the `while` loop you should be familiar with that uses the [`break`](https://docs.python.org/3.5/reference/simple_stmts.html#break) keyword:

```python
>>> n = 1
>>> while True:
>>>     n = n * 2
>>>     if n > 32:
>>>         break
>>> print(n)
64
```

Since the while condition here is `True`, which __always__ evaluates to `True`, you might think that this loop would run forever. And that's exactly what would happen if you removed the `break` statement. Using `break` will terminate the enclosing loop, allowing the program to continue executing code further down. In the example above `break` is executed once the number grows larger than 32, then program execution continues on with the `print()` statement.

## Assignments

To complete the following drills, you'll need to draw on what you just learned about lists and iteration. For each drill, you'll need to write a function that implements the required behaviors. As in the previous sets of drills, we'll be using Codewars, and there are pre-written tests you must make pass to complete the challenge.

Sample solutions are provided at the end of this assignment. Give yourself up to 20 minutes to complete each of the drills below, and if you're stuck at that point, hit [Slack](https://thinkful.slack.com/messages/data-science/) or have a look at the solutions and discuss any confusing points with your mentor. These drills are intentionally challenging, so don't worry if you struggle with them.

As in the earlier drills, make sure you're logged into Codewars when you're working through these drills. That will make it easier for you and your mentor to refer back to your code.

1. [Longest word](https://www.codewars.com/kata/thinkful-list-drills-longest-word)
1. [Grade calculator](https://www.codewars.com/kata/thinkful-list-and-loop-drills-grade-calculator)
1. [Lists of lists](https://www.codewars.com/kata/thinkful-list-and-loop-drills-lists-of-lists)
1. [Inverse slicer](https://www.codewars.com/kata/thinkful-list-and-loop-drills-inverse-slicer)


Once you've completed each drill spend a few minutes reading other solutions before moving on and compare other solutions to yours. Keep a particular eye out for different methods people use to solve the same problem you did. At your next session, be sure to spend some time talking about your answers with your mentor.

Limit yourself to 20 minutes per drill _maximum_. If you're still stuck after that time, hit [Slack](https://thinkful.slack.com/messages/data-science/) or seek enlightenment from the example solutions at the bottom of this assignment. Whether or not you're able to complete each drill on your own, be sure to spend some time talking about the drills and answers with your mentor at your next session.


###### Hey friend, we're here to help! Just a reminder that you can always check out the [Q&A sessions](https://www.thinkful.com/open-sessions/qa-sessions/) if you're stuck or have questions in between your 1-1 sessions. Feel free to drop by for a few minutes or the full hour. Happy coding!

## Sample solutions

Once you've completed these drills or spent twenty minutes working on each one, have a look at these [sample solutions](https://gist.github.com/Grae-Drake/5a7cf7a5b7712f66e4661418ff339b79). Compare and contrast your own approach.

