---
title: Function basics
author: Thinkful
team: grading
type: graded
time: 60
uuid: 1176819f-18b2-4416-979f-5eaa51604897
---

Functions are one of the most important concepts in programming. A function describes a repeatable process or behavior. You define that behavior once, and you can run and re-run your set of instructions whenever and as many times as you need.

Let's look at an example: Python's built-in [`print()`](https://docs.python.org/3.5/library/functions.html#print) function. You've already seen this function several times in each of the interactive examples so far. Check out the new example below.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/d0860d1888"></iframe>

The `print()` function above has one "*argument*", or value that is passed into the function: the string `"Hello, world"`. In the context of functions, an *argument* (or *parameter*) is a value that gets passed to the function and that the instructions inside the function have access to.


## Defining and executing functions

There are two distinct moments to consider when working with functions: when you initially *define* a function and when you *execute* (or "call") a function that has already been defined.

### Function definitions

Let's look at a function definition:
```python
def times_two(num):
    return num * 2
```
The `def` keyword signifies that a function is about to be defined. Next comes the function name (in this case, `"times_two"`). This name gives us a way to refer back to the function later.

Next is the function's *parameter list*, which are the parameters the function will expect to be passed inside to the main body of the function when the function is called. The parameter list is zero or more parameters surrounded by `(` `)` characters. In this case we're passing in a single parameter: `num`.

After the parameter list is the `:` character, which tells the Python interpreter that you're about to provide the line(s) of code making up the main body of the function. In our example our body is just one line of code: `return num * 2`.

Note that the function body is indented. This indentation gives a visual cue for what code is inside the function body and which code is outside the function. This style of indentation is best practice in most programming languages because it makes programs easier to read, but in Python indentation isn't just a good idea. _It's the law_. In Python indentation has semantic meaning. The code below, which is identical to the example above, raises a syntax error because the Python interpreter is expecting to see an indented block of code but doesn't see one:

```python
def times_two(num):
return num * 2
```

You may think that assigning semantic meaning to indentation whitespace is an odd decision, particularly if you have experience working in other programming languages that are designed differently. For example, both of the JavaScript function definitions below are identical and valid.

```javascript
function times_two(num) {
    return num * 2;
}

function times_two(num) {
return num * 2;
}
```

The advantage of giving indentation semantic meaning, though, is that we don't need to use characters like `;` to end statements or `{` and `}` characters surrounding code blocks to tell the interpreter where a code block starts and ends. We _should_ be using indentation properly anyway, so Python _enforces_ proper indentation and _uses_ that indentation to let you write code that looks more like English.

Finally, the function body includes a *return statement*, which tells the function what value to output, or "return", to the part of the program that eventually executes the function. The `return` keyword starts the return statement, followed by the value that you'd like to return.

Return statements tell your function that its job is done and will end the execution of the instructions in your function body. That means any code coming after your return statement inside the function body won't be executed.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/562adec2f8"></iframe>


### Calling functions

Once you've defined a function you have a named block of code that you can execute when you *call* the function by name. To call a function write out its name followed by parentheses `(` `)` containing the argument(s) you want to pass in. In the example above we call the `triple()` function on line 11 with `triple(5)` after having defined it earlier on lines 6 through 9. Let's look at a larger function with more going on inside.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/6d52749401"></iframe>

You don't need to understand all the code inside the body of our `variance()` function, but take a look over it to see how we're creating a list of instructions inside our function definition and then _executing_ those instructions every time we call the function. You probably wouldn't want to write the code inside this function over and over. That's where functions shine: write code once and run it as many times as you like by simply calling the function.


## A note about programming versus mathematics

The `print()` function demonstrates a key difference between functions in _programming_ and functions in _math_. In math, a function is a way to map each input onto a single output. The math function `f(x) = 2x`, for example, maps the input `3` onto the output `6` and the input `1337` onto the output `2674`. Python functions, however, are a defined set of instructions that you can call and execute. You _can_ write that set of instructions to behave like a math function and map arguments onto a return value, but that isn't necessary. In fact, Python functions don't even need to have input or output values at all. The `print()` function is an example: it displays a message to you but doesn't return any value at all.

In programming, functions that have this mathematical property of mapping arguments onto exactly one return value are called "*determinate*" functions. In general, well crafted Python functions are determinate.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/a17c5ccab2"></iframe>

Using determinate functions makes your code easier to reason about because you don't need to keep the state of the rest of your program in mind in order to know how the function will act. In the example above you have to know (or find out) what the value of `secret_number` is before you can predict how your code will act.

Speaking of state, if the state of your program affecting the output of your function means your function isn't determinate, what about the reverse case where your _function_ affects the _state_ of your program? In math that isn't possible, but since Python functions are just a collection of instructions it _is_ possible to modify state of your program. A function that modifies the state of your program is said to have *side effects*.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/624b585d31"></iframe>

In general it's better to write your functions so they don't have unneeded side effects. In fact, Python intentionally makes it difficult to modify variables outside a function's scope (more on "scope" later) by requiring you to explicitly declare you want to do that with the `global` keyword as we did in the example above.

A Python function that is _both_ determinate _and_ has no side effects works essentially like a function in mathematics. Python functions with each of these two properties are called "*pure functions*".

## Tips for working with functions.

The name `print()` is well chosen. Just knowing the name of the function gives us a good sense of what it does. As with variables, a well chosen function name can make clear what might otherwise require multiple lines of comments to explain.

Well crafted functions like `print()` have a *single responsibility*. This means that they are designed to do one thing and do it well. `print()`'s sole responsibility is to display information to the user. When you are writing functions strive to keep each one as simple and focused as possible. If you have a big function doing lots of different things it might be time to split your function up into multiple smaller functions.