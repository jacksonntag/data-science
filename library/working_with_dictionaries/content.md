---
title: Working with dictionaries
author: Thinkful
team: grading
time: 180
uuid: ff860319-7701-4394-aa70-0d574c5521e8
---

Dictionaries are a common and useful data structure that allow you to store data as an unordered collection of **key**: **value** pairs.

In this checkpoint, we'll cover everything you need to know to use Python dictionaries. This checkpoint ends with a set of drills in which you'll practice the concepts you learn here.


## Dictionaries vs. lists

While lists make sense for collecting inherently sequenced data and are designed to simplify accessing items by index number, dictionaries make sense for data you reference by _name_, or "key", rather than by _position_, or "index".

```python
greetings = {
    "english": "hello",
    "japanese": "こんにちは",
    "german": "hallo",
    "hindi": "नमस्ते",
    "leet": "h3ll0",
}

word_counts = {
    "the": 4,
    "and": 2,
    "word": 3,
    "beginning": 1,
    "god": 2,
    "in": 1,
    "with": 1,
    "was": 3,
}

```

Python dictionaries are known in other languages as "associative arrays" or "hash tables" (or "objects" in JavaScript :P), so if you've programmed in another language you likely know a lot about dictionaries.

Dictionaries may initially be less intuitive to you than lists, and you might wonder why you'd want to use a dictionary when you *could* hack a list (or maybe a multidimensional list) into doing the job instead. There are two big reasons dictionaries might be the right tool for the job:

 1. Looking up or setting values by key rather than by index has incredibly different performance implications, and
 2. Writing code that refers to data by name rather than by index number can be much clearer and easier to understand.

The first point, about performance, will almost certainly come up during your technical interview process, and, if you're writing programs with large inputs, the performance differences between lists and dictionaries can mean the difference between code that executes in less than a second versus code that will keep running for days or years.


## Creating, accessing, and modifying

The easiest way to create a dictionary is to type out items as **key**: **value** pairs in curly braces `{` `}`:

```python
greetings = {
    "english": "hello",
    "japanese": "こんにちは",
    "german": "hallo",
    "hindi": "नमस्ते",
    "leet": "h3ll0",
}
```
Each key is followed by a colon `:` and then the corresponding value. In the example above, `"japanese"` is the key and `"こんにちは"` is the value.

A key: value pair together are called an **item**. Each item is separated from the next with a comma. You'll find that you're generally using strings for your keys, though you may use any immutable object as a key.

###### We aren't covering immutability in this fundamentals course, but if you'd like to read about it see the <a href="https://docs.python.org/3.5/reference/datamodel.html">Python data model documentation</a>.

Dictionary values are accessed using bracket notation, just like with lists and strings, except that instead of using an index number you use a key:

```python
>>> greetings["japanese"]
"こんにちは"
```

Updating the value associated with a key looks very much like assigning a value to a variable:

```python
>>> stock = {"apples": 5, "oranges": 2}
>>> stock["apples"] = 20
>>> stock["oranges"] += 1
>>> stock["apples"]
20
>>> stock["oranges"]
3
```

In fact, creating a _new_ key: value pair looks the same as well. You specify the key using bracket notation and assign a value with the `=` operator.

```python
>>> stock["pears"] = 10
stock["pears"]
10
```

You can delete items from a dictionary with the `del` keyword, removing the key: value pair entirely.

```python
>>> del stock["pears"]
>>> stock["pears"]
Traceback...
KeyError: 'pears'
```


## Checking for membership in a dictionary

You can use the key to get the value of a dictionary item with bracket notation, but what if you just want to know whether a key is in a dictionary at all? For that you can use the `in` and `not in` operators.

```python
>>> greetings = {
...     "english": "hello",
...     "japanese": "こんにちは",
...     "german": "hallo",
...     "hindi": "नमस्ते",
...     "leet": "h3ll0",
>>> }
>>> "english" in greetings
True
>>> "spanish" in greetings
False
>>> "pirate" not in greetings
True
```

As you saw above when we tried to check `stock["pears"]` after deleting it, trying to look up the value for a key that isn't in the dictionary will raise a `KeyError`. These boolean operations are useful for working with dictionaries without raising `KeyError`s.

Now that you know how to create and modify dictionaries, take a few minutes to play around with the code below.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/2fbd1c8139"></iframe>


## Methods and looping

There are three important dictionary methods you should know that map onto the three main concepts of dictionaries: **keys**, **values**, and **items**.

The `.keys()` dictionary method will return all the keys in a dictionary.

The `.values()` method will return all the values in a dictionary.

The `.items()` method will return all the key: value pairs (or "items") in a dictionary.

Let's look at examples of all of these.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/0ed97bb313"></iframe>

Each of these methods returns a **dictionary view object** that looks and acts a lot like a list but is actually a different kind of object. There are just two points we'll cover about view objects right now. First, you can easily convert them into real lists with the built-in `list()` function if you need a list.

```python
>>> stock = {"apples": 5, "oranges": 2}
>>> list(stock.keys())
["apples", "oranges"]
```

And second, view objects provide a _dynamic view_ of the underlying dictionary, so if you update the dictionary then the view object will show you the updated data:

```python
>>> stock = {"apples": 5, "oranges": 2}
>>> items_for_sale = stock.keys()
>>> stock["pears"] = 10
>>> items_for_sale
dict_keys(['pears', 'oranges', 'apples'])
```

For more information on dictionary view objects check out the [Python documentation](https://docs.python.org/3/library/stdtypes.html#dictionary-view-objects) or see this [Stack Overflow question](http://stackoverflow.com/questions/8957750/what-are-python-dictionary-view-objects) for a discussion of the difference between these dictionary methods in Python 2 and Python 3.

It's important to say again that dictionaries and their view objects are *unordered*. None of the items come before or after any of the other items. Printing out a dictionary or view objects will display the items in an essentially arbitrary order, and even in a different order when you print it different times. The same is true of the values generated by `.keys()`, `.values()`, and `.items()` above: the elements can come out in an arbitrary order. You won't know and shouldn't rely on them being in a particular order. If you _need_ to look at collection of keys, values, or items use the built-in `sorted()` function on your relevant view object to create an ordered list:

```python
>>> stock = {"apples": 5, "oranges": 2, "bananas": 4}
>>> list(sorted(stock.keys()))
["apples", "bananas", "oranges"]
```

## Assignments

These drills cover dictionaries as well as the other concepts you've covered so far. Again, for each drill you'll need to write a function that implements the required behaviors and passes the pre-written test suites.

Sample solutions are provided at the end of this assignment. Give yourself up to 30 minutes to complete each of the drills below, and if you're stuck at that point, hit [Slack](https://thinkful.slack.com/messages/data-science/) or have a look at the solutions and discuss any confusing points with your mentor.

As in the earlier drills, make sure you're logged into Codewars when you're working through them. That will make it easier for you and your mentor to refer back to your code.

1. [Order filler](https://www.codewars.com/kata/thinkful-dictionary-drills-order-filler/)
1. [User contacts](https://www.codewars.com/kata/thinkful-dictionary-drills-user-contacts)
1. [Multiple modes](https://www.codewars.com/kata/thinkful-dictionary-drills-multiple-modes). This drill is particularly challenging. If you're struggling with it, think about how you might use a dictionary to keep track of the number of times each letter appears in a string, using the character as the key and using the count as the value.

Once you've completed each drill spend a few minutes reading other solutions before moving on and compare other solutions to yours. Keep a particular eye out for different methods people use to solve the same problem you did. At your next session, be sure to spend some time talking about your answers with your mentor.

Limit yourself to 30 minutes per drill _maximum_. If you're still stuck after that time, hit [Slack](https://thinkful.slack.com/messages/data-science/) or seek enlightenment from the example solutions at the bottom of this assignment. Whether or not you're able to complete each drill on your own, be sure to spend some time talking about the drills and answers with your mentor at your next session.


###### Hey friend, we're here to help! Just a reminder that you can always check out the [Q&A sessions](https://www.thinkful.com/open-sessions/qa-sessions/) if you're stuck or have questions in between your 1-1 sessions. Feel free to drop by for a few minutes or the full hour. Happy coding!

## Sample solutions

Remember, reading other people's code is one of the most effective ways to improve your programming skills. Once you've completed these drills or spent thirty minutes working on each one, have a look at these [sample solutions](https://gist.github.com/Grae-Drake/0d614c775af649d620b54a21180c32dc). Compare and contrast your own approach.
