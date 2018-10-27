---
title: Data types
author: Thinkful
team: grading
time: 90
uuid: d410472b-765f-4b55-8dbc-d3e0e21c5850
---

Variables can represent different *types* of values. For example, words and numbers are different types of data. A variable could refer to the number `42` or it could refer to the words `"forty two"`. You can do math with the first one, but trying to subtract `5` from `"forty two"` in Python isn't going to fly.

Python has many [built-in](https://docs.python.org/3.5/library/stdtypes.html) data types and we're going to cover some common ones now: "**strings**", "**numbers**" (including integers and floats)", "**booleans**", and "**`None`**". Later in this Unit we'll explore each of these in more detail. Right now we'll give you a brief introduction to each. The goal here is to give you a lay of the land and a chance to tinker, not for you to memorize all the information in this reading.

After that, we'll discuss the idea of *conversion*, which has to do with how we transform data from one type to another in Python.


### Strings

*Strings* are textual data delineated by opening and closing quotes. Either single or double quotes is fine, but both the opening and the closing quote must be the same kind: `food = 'pizza'` and `food = "pizza"` are both valid.

Words, names, book chapters, emails, text files, all of these are textual data and can be represented by strings. When you get down to it much of our data is just a bunch of characters strung together in a particular order.

Read through the code below, then go back and fiddle with it and rerun it to get a sense for what's going on.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/1b290984fe"></iframe>

We'll explore strings in depth later in this Unit.


### Numbers: integers and floats

Numbers come in two main flavors in Python: *integers* (or "ints") and *floating point numbers* (or "floats").

Integers represent, well, integers: whole numbers that aren't written as a fraction or with a decimal point. There is no maximum integer size: Python 3 can handle integers that are arbitrarily large (unlike many other languages).

Floating point numbers are numbers that *do* include a decimal point. Floats in computer science are a fun topic. Since computers represent everything internally in binary, and since it's impossible to precisely represent many decimal fractions in binary, it's easy to end up with floating point issues like this:
```python
>>> .2 + .4
0.6000000000000001
```
That happens because it's impossible to represent `.2`, `.4`, and `.6` precisely in binary, so there's a limit to how precise we can get. We won't get into the nity-gritty with floating point numbers, but know that doing arithmetic with floats is asking for trouble. See [here](https://docs.python.org/3.5/tutorial/floatingpoint.html) for more information on floats in Python 3 if you're interested.

Unlike strings, you can do math with numbers!

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/ebc39b9c20"></iframe>

We'll explore the properties and operations of ints and floats in depth later.


### Booleans

*Booleans* signify truth and falsity. A boolean has just two possible values: `True` and `False`.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/11d1a6c5f2"></iframe>

In the example above, we set `logged_in` to True, and we then have a block of code that runs if and only if the user is logged in. We also have a block of code that only run if `logged_in` is set to `False`, and another block that runs for any other non-boolean value. Tinker around with the example to see if you can get all three responses to run.

We'll learn more about Booleans in the lesson on application logic.

### `None`

Strings, numbers, and booleans are useful for representing actual _things_, but sometimes you want to represent _nothing_. That is, you want to represent the _absence_ of any value. For that Python gives us *`None`*.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/168a24f627"></iframe>

You could have a deep philosophical debate about when it's appropriate to use `None` instead of `False` or `0` or an empty string `""` or so on. We won't have that debate here. Just know that `None` is around to use when you want to represent the lack of a value.


## Type conversion

To close out this assignment, we want to make you aware of the idea of *converting* data of one type to data of another. In Python, if you try to perform an operation that expects a number on a string you'll get an error. For example, if you try to subtract the string `"10"` from the number `42` you'll get an error.

```python
>>> 42 - "10"
TypeError: unsupported operand type(s) for -: 'int' and 'str'
```
That `TypeError` is telling you that you're trying to use data of a particular type (a string) that the `-` operator doesn't support. We can fix that by converting the string to an integer with the built-in [`int()`](https://docs.python.org/3.5/library/functions.html#int) function or convert it to a float with the built-in [`float()`](https://docs.python.org/3.5/library/functions.html#float) function:

```python
>>> 42 - int("10")
32
>>> 42 - float("1.5")
40.5
```

Similarly, you can't use the `+` operator to concatenate a number with a string.
```python
>>> "Number of magic beans: " + 42
TypeError: Can't convert 'int' object to str implicitly
```
This error is telling us that we're trying to perform an operation, concatenation, on integer data that doesn't support that operation. Again, we can fix that error by converting the number to a string with the built-in [`str()`](https://docs.python.org/3.5/library/functions.html#func-str) function:

```python
>>> "Number of magic beans: " + str(42)
'Number of magic beans: 42'
```

That does it for the basic data types we'll cover now. Next up we'll look at different ways to collect multiple pieces of data into one convenient structure.

