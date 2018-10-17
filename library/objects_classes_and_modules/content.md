---
time: 120
name: 'Objects, classes, and modules'
uuid: cf51d657-2137-42a4-99e6-dab1a2b41ac9
---

It's time to talk about something you've been using every time you write Python, but that you may not have been thinking about: objects.

You've been using objects all along because _everything in Python_ is an object. Integers? Objects. Strings? Objects. Lists, dictionaries, booleans... even functions. All of these are objects.

Objects and "object-oriented programming" are deep topics that cut to the core of Python and computer science. But as a practical matter, data science isn't a very object-oriented discipline, so we won't dive deep into object oriented programming practices.

Instead, we have two pragmatic goals for this checkpoint. First, we'll peer behind the surface of objects so that you have better understanding of how your tools work. Second, we'll introduce classes and modules so you'll be comfortable creating your own custom objects and modules.

At the end of this checkpoint, you'll work through a set of drills to reinforce what you've learned.


## What are objects?

Of course, saying "everything in Python is an object" doesn't tell you much about what an _object actually is_. Python **objects** are collections of attributes. Each attribute has a name and a value. You might be thinking that attributes of an object seem a lot like the items of a dictionary. You'd be right.

In addition to attributes, each object has a unique id, which you can access with the built-in [`id()` function](https://docs.python.org/3/library/functions.html#id), and a **type**, which you can access with the built-in [`type()` function](https://docs.python.org/3/library/functions.html#type).

We can get a list of the names for each attribute of an object by passing the object into the built-in `dir()` function. Let's try that with the integer `1` to see what `1` _really_ looks like.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/36239027a0"></iframe>


That's... a lot of attributes for something you might think was just the simple number "one". What are these mysterious attributes?


## Accessing and using attributes

Well, let's find out what these attributes are by accessing them. You can access object attributes using dot notation: follow the object with a `.` and then the name of the attribute you want to access. Let's try this with a string. If we call `dir()` on a string we see one of the attributes is `upper`. Let's access that.

```python
>>> "hello".upper
<built-in method upper of str object at 0x1015715e0>
```

Oh, that's right, we saw earlier that strings have a method called `.upper()`. You might have even used it to solve one of the earlier string drills. Let's call that method on our string by adding `()` to the end.

```python
>>> "hello".upper()
'HELLO'
```

Just as you've been using objects this whole time without necessarily knowing that they've been objects, you've been accessing object attributes by using methods like the string method `.upper()` and the list method `.append()` without necessarily knowing that they were attributes of your object. "Method" is in fact just the special name we use for functions that are attached to an object as one of the object's attributes.

If you tinker around with the different attributes of different objects you'll see the values are very frequently functions. Attributes don't have to be functions, though. Sometimes they're other values.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/93e559e4b8"></iframe>


These attributes are pretty cool, but where do they come from? Let's find out.


## Abstraction and inheritance

Let's think about abstraction for a moment. Consider the statement `1 + 2` and the statement `1 + 'pizza'`. We expect the first statement to work because both operands are _numbers_, and we (rightly) expect the second statement to fail because you can't add a number and a string. The operands in the second example aren't _the same type of thing_.

What do we mean when we say a number and a string aren't "the same type"? Similarly, what do we mean when we say something like "integers are a type of number"?


In both cases above we're making abstractions. Each integer has a whole bunch of attributes it shares with other integers, attributes it doesn't necessarily share with a string. For example, numbers can be even or odd, composite or prime, but those concepts don't even make sense when talking about strings.

Similarly, different types of numbers share some attributes but not others. All integers are divisible by one, but other types of real numbers (like floats) don't have that attribute. "Number" is an abstract class that both integers and floats belong to, even though they're different from one another.

In all of these cases we can intellectually abstract away from specific instances of something (like `1` and `10` and `42`) to create a "class" (in this case, integers) where we list out all the attributes that the instances share with one another. Whenever we chose a specific instance of the class you know that the instance inherits all of the properties of the class it belongs to.

All of this talk about abstraction is a bit heady, so let's look at the way Python creates different types of numbers using **classes** as a concrete example.

Integers and floats are both a type of number. Python has a [numbers class](https://docs.python.org/3/library/numbers.html#numbers.Number) that ints and floats belong to. They inherit the attributes of that class. Rational numbers are another type of number. Integers are rational numbers but floats aren't, so integers inherit the attributes of the [rational class](https://docs.python.org/3/library/numbers.html#numbers.Rational) but floats don't. You can read more detail about this and related numeric classes [here](https://docs.python.org/3/library/numbers.html), but the takeaway is that Python classes give us a way to define a type of object and allow all objects of a certain type to inherit the attributes of their class. All the unexpected attributes you saw on the object `1` above are inherited from the classes it belongs to.

## Custom objects

As a data scientist you can keep on using all of Python's built-in objects and the objects you import from the standard library and other modules (more on importing modules next) without needing to worry too much about making your own custom objects. But seeing how custom objects work will help you understand objects in general, so we'll look at an example of setting up your own custom objects.

Let's say you want to model a bunch of quarks. Each of your quarks will have its own color (red, green, or blue) and flavor (up, down, strange, charm, top, or bottom). All quarks will have the same baryon number (`1 / 3`) and will have a method to interact with another quark by exchanging colors (modeling the strong interaction).

Before you can start churning out quarks you first define what you _mean_ by quark, or, in Python terms, you need to define the `class`. Let's see what that class might look like

```python
class Quark(object):

    def __init__(self, color, flavor):
        self.color = color
        self.flavor = flavor

    baryon_number = 1 / 3

    def interact(self, other_quark):
        self.color, other_quark.color = other_quark.color, self.color

    def __repr__(self):
        return "{} {} quark".format(self.color, self.flavor)
```

Let's break down this example piece by piece. In the first line we use the `class` keyword to start the definition of a new class. This works just like the `def` keyword when defining new functions. After that comes the name of our new class (`Quark`). It's customary to use "[CapWords](https://www.python.org/dev/peps/pep-0008/#class-names)" capitalization with custom classes. We follow the class name with parentheses containing the class we want "subclass" from. If you don't have a more specific class you'd like to subclass, the built-in `object` object has the most basic default attributes you want to inherit.

Inside the class definition we define three methods (`__init__()`, `interact()` and `__repr__()`) and the `baryon_number` attribute. Each object that we create from this class will inherit these attributes. The `interact()` method implements the color exchange we set out to do, while `__init__()` and `__repr__()` are special double-underscore or "dunder" methods.

The `__init__()` method is special. Python automatically calls an object's `__init__()` method when it's created. That means all of the code inside runs as a part of setting up each new object. In our example we're setting two attributes: the quark's color and the flavor.

"But wait", you say, "what about the first `self` argument?" Good question. In an object, the `self` variable is used to refer to the object itself. Every method expects `self` as the first argument, and whenever you call a method `self` is passed in behind the scenes without you having to explicitly include it in your method call. When you're reading code that includes `self` you can mentally replace that with "the particular object I'm dealing with", so in English `self.color = color` would read as:

>The color of the particular quark I'm dealing with is the value of `color` passed into `__init__()`.

Let's create a couple of quarks and play around with them.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/1ef57311a4"></iframe>

Unlike color and flavor, each quark has the same baryon number, so we can set that outside the `__init__` function just like we do for the method attributes.

The `interact()` method is a straightforward function that manipulates both the object calling it and the object passed in as an argument. The `__repr__()` method is another useful dunder method that tells your object how to play nice with `print()` and other cases that require a representation of your object.

Take a minute and go back to the interactive example above to see if you can add a `spin` attribute to the class definition, then run your code and see if it works, or, if there's an exception, if you can run down the cause. In physics quarks can have a spin of either `1 / 2` or `-1 / 2`.

You've already seen and used a number of powerful built-in Python functions and objects, but there are worlds of additional functionality you can rope in whenever you want.

Your Python installation almost certainly includes the entire "[standard library](https://docs.python.org/3/library/)": a library of modules that aren't loaded by default but that are available for you to import whenever you like.

In addition to the standard library, there is a vibrant ecosystem of open-source Python modules that you can download, install, and import into your programs. The best centralized reference for these is the [Python Package Index](https://pypi.python.org/pypi), or "PyPI". For example, here is the [PyPI page for Pandas](https://pypi.python.org/pypi/pandas/0.19.2), a module you'll use heavily as a data scientist. We'll install and dig into Pandas and other packages soon.


## Importing modules

All you need to start using modules is an `import` statement at the top of your program. Here's how you'd import the built-in `math` and `random` modules

```python
import math
import random
```

It's customary to put your import statements at the [top of your files](https://www.python.org/dev/peps/pep-0008/#imports).

Once imported, you'll have access to a `math` module object and a `random` module object. Just like every object, these contain attributes that you can work with. Some interesting attributes are the [`math.pi` constant](https://docs.python.org/3/library/math.html#math.pi) and the [`random.choice()` method](https://docs.python.org/3/library/random.html#random.choice). Let's tinker with these

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/c41a6600bf"></iframe>

Refer back to the documentation for `math` and `random` linked above, find a couple of attributes you'd like to play with, and use them in the interactive example. For extra credit, find a new package in the standard library that you'd like to import and play with.


## Other packages

Other packages are imported just like modules in the standard library once you have them installed in your local Python environment. In this fundamentals course, we'll use the NumPy, Pandas, matplotlib and SciPy packages. You'll notice import statements like this a lot once we start doing real work:

```
import numpy as np
import scipy as sp
import pandas as pd
import matplotlib.pyplot as plt
```


## Custom modules

Creating your own modules is easy once you're working with files on your local machine. In fact, every Python file (file with a `.py` extension) is also a module. The module name is the name of the file minus the `.py` part, so if you have a file called `demo.py` you can import it with `import demo`. All of the variables and functions in your file are available as attributes of the module. 

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/6eb6ca9300"></iframe>

## Executable scripts

Sometimes you'll want to be able to execute a module from your command line as a script. We won't get into the [details](https://docs.python.org/3/tutorial/modules.html#executing-modules-as-scripts) here, but you can add this code to the end of your module:

```python
if __name__ == "__main__":
    # Call functions here that you define above.
```

and all of the statements inside the `if` statement will be run when you call the module from your command line with `python [your module name].py`


## Assignments

These drills touch on the object topics we've covered in this lesson. Again, for each drill you'll need to write a function that implements the required behaviors and passes the pre-written test suites.

Sample solutions are provided at the end of this assignment. Give yourself up to 30 minutes to complete each of the drills below, and if you're stuck at that point, hit [Slack](https://thinkful.slack.com/messages/data-science/) or have a look at the solutions and discuss any confusing points with your mentor.

1. [Vectors](https://www.codewars.com/kata/thinkful-object-drills-vectors).
1. [Puzzlebox](https://www.codewars.com/kata/thinkful-object-drills-puzzlebox)
1. [Quarks](https://www.codewars.com/kata/thinkful-object-drills-quarks)

Once you've completed each drill spend a few minutes reading other solutions before moving on and compare other solutions to yours.

Limit yourself to 30 minutes per drill _maximum_. If you're still stuck after that time, hit [Slack](https://thinkful.slack.com/messages/data-science/) or review the example solutions below, then talk with your mentor about these drills at your next session.


## Sample solutions

Once you've completed these drills or spent thirty minutes working on each one, have a look at these [sample solutions](https://gist.github.com/Grae-Drake/d0dd062d52a2fbac1d8712c74c3af4c7). Compare and contrast your own approach.

