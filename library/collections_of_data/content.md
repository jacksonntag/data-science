---
time: 30
name: Collections of data
type: written content
---


So far all of the things we've stored in a variable have been one single value, whether that value is a string like a name or an integer like a score or so on. Sometimes you'll want to collect several such things together into a single variable. Python gives you several great built-in data structures for doing that. In this assignment we'll cover the two most used: lists and dictionaries.

### Lists

*Lists* are ordered collections of data. To create a list simply wrap other data, separated by commas, in square brackets `[` and `]`:

```python
inventory = ["beans", "coin", "tome"]
tome_dimensions = [8.5, 11, 2]
```
You can put any value into a list that you like, even another list. Just like the characters in a string, the elements in a list are _ordered_ and can be accessed by index with bracket notation.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/59b7d426d9"></iframe>

### Dictionaries

*Dictionaries* are another way to collect several pieces of data together. While a list stores that data as an ordered sequence, dictionaries store that data as an _unordered_ collection of *key-value pairs*.

To create a dictionary, wrap key-value pairs in curly braces:

```python
adventurer = {"name": "grae", "profession": "magician"}
```

In the example above `"name"` and `"profession"` are the *keys*, while `"magician"` is the *value* associated with the `"profession"` key and `"grae"` is the value associated with the `"name"` key. Each key is separated from its value by a colon `:`, and each key-value pair is separated from other pairs with a comma `,`.

Just like lists, you can use bracket notation to access the data in a dictionary. Unlike lists, where you use an index number, with dictionaries you look up data using a particular key.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/8072bc7067"></iframe>
