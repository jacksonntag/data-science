---
title: Working with variables
author: Thinkful
team: grading
type: graded
time: 60
uuid: 3323613f-6bdd-44c3-8a7c-02cf336b24ab
---

A variable is a name that is attached to a value. Variables open up two possibilities for us as programmers.

First, they give us a shorthand way to refer to values created elsewhere in a program. We can declare and define a variable once, then pass that value around in our code without having to rewrite the value each time.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/6edd91e237"></iframe>

Second, variables give us a way to manage *state* in a program. *State* has to do with persisting or modifying values over time. That probably sounds abstract, so let's look at a concrete example. Consider the following interface, which asks the user how many bottles of beer are on the wall (super useful, right!?):

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/acecbf9a2d"></iframe>

Take a minute to read through the code comments in the Python code in this example to get a sense of what it's doing. Remember, the goal at this moment is not to master the syntax or understand every piece of code; instead, we want you to start get a feel for this idea of *state*.

In this simple program, the application state is maintained in a single `bottle_count` variable. The user sets the initial value when the program starts, and can choose to modify it later. We say that in between prompts to modify its value, the application's state is maintained in the `bottle_count` variable. At any point when this program is running, the `bottle_count` variable tells everyone else how many total bottles exist. Variables give us a way of persisting this information for the life of the program.

## Variables in Python

There are two distinct moments to think about when working with variables in Python: assigning a value to a variable, and retrieving the value from a variable.

To assign a value to a variable we use the `=` operator with the following syntax:

```python
my_name = "Guido van Rossum"
```

Here we've said that the value of the variable `my_name` is `"Guido van Rossum"`, and that information is stored in memory. We could update the value of `my_name` by adding another line using the assignment operator (for instance, a line that says `my_name = 'John Cleese'`).

###### It's important to note that the <code>=</code> operator is <em>assigning a value to a variable</em>, not <em>asserting that two different values are equal</em>. When you see the <code>=</code> character in mathematical statements it's an "equals sign", and means that the value on both sides are equal. For example: <code>2 + 2 = 4</code> is a perfectly reasonable mathematical statement. But that's <em>not</em> how <code>=</code> works in Python. In Python the <code>=</code> character is an <em>operator</em> that <em>assigns</em> the value on the right to the variable on the left. Trying to execute the line of code <code>2 + 2 = 4</code> in Python will give you a syntax error because you can't "assign" anything to the value <code>2 + 2</code>. Mixing up the math usage of <code>=</code> with the programming usage of <code>=</code> is one of the most common errors for beginner programmers and one you will probably make several times.

To access the value in a variable, you simply refer to the variable in your code. This example would print a greeting that accesses and uses the value of `my_name`:

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/e33c3fde2a"></iframe>

## Naming variables

The names you choose for variables are important.

On the one hand, there are some rules about how variable names *must* look in order for the Python interpreter to recognize that our code is talking about a variable in the first place. On the other hand, there are stylistic conventions about how we *should* name our variables.

### The rules

The naming requirements in Python are simple:
 1. Variable names must start with a letter or an underscore,
 2. The remainder of your variable name may include letters, numbers, and underscores, and
 3. The variable name cannot be a *reserved word*.

All of the following are valid variable names:
```python
name = "Guido"
favorite_painter = "Mondrian"
__password__ = "hunter7"
job1 = "Programmer"
job2 = "Benevolent Dictator"
```
Each of the variable names below is invalid and will raise a syntax error:

```python
# Variable name doesn't start with a letter or underscore:
1st_name = "Guido"

# Variable name includes a disallowed character: `-`:
my-password = "hunter2"

# Variable names can't be keywords like `else`:
else = 1
```

*Reserved words* are a special category of words that you're not allowed to use as variable names in a given programming language. For instance, in Python, you can't reassign the name `True` or the word `def` to a new value. See the documentation for the full list of [33 reserved words](https://docs.python.org/3.5/reference/lexical_analysis.html#keywords).

### The recommendations

In addition to the syntax rules above there are also recommended best practices that you *should* follow. Ignoring these recommendations won't cause your code to break, but it will make your code look strange to other Python developers and make it harder to maintain. [PEP 8](https://www.python.org/dev/peps/pep-0008/) contains most of the relevant Python style recommendations. Here are a few important ones:

* **lower_case_with_underscores**: Python developers generally use *lower_case_with_underscores* (sometimes called "snake case") for variable names. For example: `this_is_snake_casing`. A Python variable name should have lower case letter throughout with words separated by an underscore `_` character. There are cases where we use TitleCasing ([with classes for instance](https://www.python.org/dev/peps/pep-0008/#class-names)) or ALLCAPS ([for constants](https://www.python.org/dev/peps/pep-0008/#constants)), but the general rule is to use snake casing.

* **Choose meaningful variable names**: When we choose variable names in Python, we should choose names that describe the underlying value and reflect how the variable gets used in the program. A well chosen variable name can help other people reading the code to understand how the variable is intended to be used. For example, full words are generally better than single characters or abbreviations:

```python
# Bad:
p = 0
n = "Guido van Rossum"
b_btls = 99

# Good:
position = 0
name = "Guido van Rossum"
beer_bottles = 99
```
Naming variables is more of an art than a science[,](http://martinfowler.com/bliki/TwoHardThings.html) and you'll get better at it over time. But as a general rule of thumb, the more your code reads like an English sentence the better you've chosen your variable names.

For additional resources on style issues you can dive into [PEP 8](https://www.python.org/dev/peps/pep-0008/) and follow it up with this fantastic talk on PEP 8 and good practices by Python contributor [Raymond Hettinger](https://medium.com/@drb/pep-8-beautiful-code-and-the-tyranny-of-guidelines-f96499f5ac17#.y7fi2ew7h).

