---
title: Working with files
author: Thinkful
team: grading
time: 60
uuid: ca522d53-64d5-4b55-8d97-1f2d21791324
---

In the examples so far, we built Pandas data frames by manually typing or pasting in text. Doing that with actual data sets would be tedious or impossible, so you'll almost always be loading your data into Pandas from files (like CSV files), from the web using APIs, or from databases and other large data stores.

We'll cover APIs and databases in later modules in this program. In this checkpoint, we'll show you how to load CSV, JSON, and XML files you've generated or downloaded into Pandas. We'll also briefly discuss working with files using vanilla Python.

When your files are well-encoded and correctly formatted and your data is clean, loading files is pretty straightforward. But that's not always the case. Dealing with malformed data is one of the largest challenges of being a data scientist, and there's no one-size-fits-all solution. Here we're going to cover the easy cases and point you towards further reading if you need it for your capstone. Your goal in this assignment is not to memorize the process for dealing with every use case, but to get an overview of the process, be comfortable working with simple files, and have a reference that you can come back to later if and when you need it.

We'll give you several example files to play with in this assignment. Go ahead and create a directory on your computer now where you'll store these files. You can download a zip with each example [here](https://gist.github.com/Grae-Drake/89c19c54077b818ea69d314e74bb6fbf), or download each file one by one below.

## Opening files with Pandas

### CSV files

**CSV** files, or "Comma Separated Values" files, are a common file format for **structured** tabular data. They're easy to produce from Microsoft Excel, Google Sheets, and Python scripts. They're also simple to work with: you can open and read them in any text editor. If you do that you'll see that a CSV is just a text file where the values in each column are separated by commas, and the rows are separated from one another with newlines. Because of their convenient structure and simplicity CSV's are extremely common to work with.

Here's a sample CSV file with the same [purchase data](https://gist.githubusercontent.com/Grae-Drake/89c19c54077b818ea69d314e74bb6fbf/raw/b259f6241c5ca9c5a3b6235bdfb260eb0d99314f/purchases.csv) you saw in the previous assignment. If you don't have it already, save a copy of this file by right-clicking in your browser and choosing "Save As". Name it `purchases.csv` and place it in the same directory as your Python files.

The basics of loading a CSV into Pandas are simple. You can load the `purchases.csv` file you just saved with this one-liner:

```python
>>> import pandas as pd
>>> df = pd.read_csv('purchases.csv')
>>> print(df)
  Unnamed: 0 country  ad_views  items_purchased
0     George      US        16                2
1       John     CAN        42                1
2     Thomas     CAN        32                0
3      James      US        13                8
4     Andrew     CAN        63                0
5     Martin      US        19                5
6    William      US        65                7
7    Zachary      US        23                3
8    Millard     CAN        16                0
9   Franklin      US        77                5
```

The Pandas `read_csv()` method takes a string representing the path to the file you want to read and returns a data frame object. In the example above the CSV file we're working with is in the same directory as the script we're running. If you saved your file elsewhere or with a different name you'll have a different path than `'purchases.csv'`.

Try loading `purchases.csv` in your own Jupyter notebook now. If your environment isn't set up for that yet or you're running into trouble you can play with this [interactive example](https://trinket.io/library/trinkets/27033bfb61).

The only required argument for `read_csv()` is the file path, but there are dozens of optional keyword arguments available that are useful in different contexts. You can read about those in [the documentation](http://pandas.pydata.org/pandas-docs/stable/io.html#csv-text-files).

Working as a data scientist you'll frequently want to output data to a file. CSV's are likely your best bet for that. To create a CSV file and write your data frame to it use `.to_csv()`:

```python
>>> df.to_csv('my_data.csv')
```

The only argument passed in to `.to_csv()`above is the path for the file you'd like to output, but there are a number of [optional keyword arguments](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.to_csv.html) you can use to tweak your output file. You can also omit the path entirely to skip the file creation and return a string that you could paste or pipe elsewhere.

Time for you to give this a shot. Choose a file name and location where you'd like to output a CSV. Look over the `.to_csv()` options linked above and choose some options you'd like to tinker with. Then, using the appropriate path, your data frame in your Jupyter notebook, and the options you've chosen, create a CSV file. Find and open your file using your favorite text editor. Did it work? Does everything look like you'd expect?

### JSON

While CSV files give you a nice (but rigid), built-in tabular structure with rows and columns, other common formats like JSON and XML allow for more customizable and flexible data storage. Unlike raw _unstructured_ text, JSON and XML _do_ have some structure requirements and are known as **semi-structured** files. 

This flexibility of semi-structured data often comes at the cost of additional complexity. JSON data can be deeply nested and may take substantial processing before you can get it into the form you want to work with. We'll cover that in more detail in the bootcamp. For now we'll give you the same purchases data you've been using in JSON format. If you don't already have it, download this [purchases.json](https://gist.githubusercontent.com/Grae-Drake/89c19c54077b818ea69d314e74bb6fbf/raw/27aba85593a688b47ec141d0d6e7f60a9e9d33a9/purchases.json) file.

**JSON** stands for "JavaScript Object Notation" and is a way to represent a JavaScript object as a string. "Objects" in JavaScript are just collections of key-value pairs, _exactly like Python dictionaries_. Almost everything you know about Python dictionaries translates directly to JavaScript objects, so you can imagine that "JSON" stands for "Python Dictionary Notation" and treat JSON as if it's a string representation of a Python dictionary.

Like CSV files, JSON files are human readable and you should be able to open and explore them with your favorite text editor. This is particularly useful when you work with new JSON and you aren't sure how it's structured. Opening files in your text editor can get tricky with very large JSON files which are too big to fit in your computer's memory, but we won't worry about that for now.

You can create a data frame from a JSON file with `read_json()`:

```python
>>> import pandas as pd
>>> df = pd.read_json('purchases.json')
```

Again, the only required argument is the file path, but you can pass in other keyword arguments to run `read_json()` with different options. [See the docs](http://pandas.pydata.org/pandas-docs/stable/io.html#json) for more details, and look into `pandas.io.json.json_normalize()` for [normalizing](http://pandas.pydata.org/pandas-docs/stable/io.html#normalization) nested JSON.

Try loading `purchases.json` in your own Jupyter notebook, or see this [interactive example](https://trinket.io/library/trinkets/c8aef0fa91) if needed.

You should generally prefer CSV for outputting your data frames into files, but you _can_ use `.to_json` to output a data frame as a JSON file:

```python
>>> df.to_json('my_data.json') 
```

The more common use case is to send JSON data over the web. For that we'd call `to_json()` without a path argument to create a JSON string that we'd later process and send:

```
>>> serialized_purchases = df.to_json()
```

We'll cover networking and using JSON like this in the bootcamp. If you'd like a preview of that check out the **Requests** module, [the only _Non-GMO_ HTTP library for Python](http://docs.python-requests.org/en/master/).


### XML

**XML**, or "eXtensible Markup Language", like JSON, is a hierarchical semi-structured data format. They are both widely used to transfer data over the web, but the newer JSON format is more common these days than the older and clunkier XML format. If you've worked with HTML then the XML syntax of opening and closing tags wrapping, or "marking up", data will be familiar. Here's an XML file with our purchases data: [purchases.xml](https://gist.githubusercontent.com/Grae-Drake/89c19c54077b818ea69d314e74bb6fbf/raw/a0b46f7f996dd0c5e6a7bfdd9af192108f3f3060/purchases.xml).

Pandas doesn't have an XML equivalent to `read_csv()` and `read_json`, so we'll use the `xml` module from the Python standard library to read in XML files and convert them to an element tree. Once we have an element tree we'll manually process it into a list that we can feed into Pandas.

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/3cc09fe849"></iframe>


The custom `xml_to_list()` function above is designed for the specific XML file we're working with. If you're working with differently structured XML then you'll need to iterate over your XML tree differently.

We aren't going to go into detail here about element trees and iterating over tree objects. You can read more at the official [xml.etree.ElementTree tutorial](https://docs.python.org/3.6/library/xml.etree.elementtree.html) if you like. If you find yourself working with XML in any detail you'll want to check out the [lxml package](http://lxml.de/index.html), a fast and useful collection of tools for working with XML.

As a data scientist you frequently don't get to choose the format of data files you're given, which is why we're covering XML here. When _generating_ data files you should probably avoid XML because it can take more work to process. CSV's are the top choice for writing data to a file. If you need a semi-structured format, prefer JSON over XML.


## Python `open()`

Each of the file loading techniques we covered above are package-specific ways to open and load files of one particular type (CSV, JSON, XML). Python offers a more general-purpose way to open any files you like with the built-in `open()` function. Here's a simple text file for you to play with if you don't already have it: [poem.txt](https://gist.githubusercontent.com/Grae-Drake/89c19c54077b818ea69d314e74bb6fbf/raw/27aba85593a688b47ec141d0d6e7f60a9e9d33a9/poem.txt)

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/4f3d19d76f"></iframe>

In the example above we use the [`open()`](https://docs.python.org/3/library/functions.html#open) function to create a **file object** that we can then work with. We then use the `.readlines()` method of the file object to create list of strings, where each element of the list is a line of text from our input file. You can read more about `.readlines()` and other file object methods in the [I/O documentation](https://docs.python.org/3/library/io.html#i-o-base-classes).

Opening a file with `open()` will _leave it open until you close it_. The `.close()` file object method will close a file. It's super easy to forget to manually close files, which can keep resources tied up and cause unexpected trouble. Luckily, Python gives us the [`with`](https://docs.python.org/3/reference/compound_stmts.html#with) statement you see used above so we don't have to remember to use `.close()`, because files opened in a `with` statement will _automatically_ be closed once the `with` statement exits. Using `with` when manually opening files is best practice and you should plan on doing that each time you use `open()` unless you have a compelling reason not to.

Almost all of the data files you produce as a data scientist will be CSV or JSON files, so we won't cover using built-in Python I/O to write to files. If you'd like additional resources on any of these topics check out the [reading and writing files](https://docs.python.org/3/tutorial/inputoutput.html#reading-and-writing-files) section of the official Python tutorial.


## A word about encoding

All of the files you've worked with seem to be made of human-readable characters, but when you get down to it everything is stored as bits, collections of ones and zeros. Which of course raises the questions: how do you know which characters you can use, and how do you translate the ones and zeros into those particular characters?

Today there is a clear answer: Unicode and UTF-8. All strings in Python 3 are **Unicode** strings, and [**UTF-8**](https://en.wikipedia.org/wiki/UTF-8) is the default encoding Python uses whenever possible. However, you're certain to run across files created with different encodings, whether that's because the files are old, the software used to create them is old, or because the [proprietary software used to create your CSV files](http://stackoverflow.com/questions/508558/what-charset-does-microsoft-excel-use-when-saving-files) is mired in legacy cruft. Unfortunately, it's not possible to automatically determine a file's encoding and then decode it correctly. When encountering encoding errors you'll need to make educated guesses about the likely encoding and use trial and error to test.

As hinted above, Microsoft Windows is a big culprit here. English-language versions of Windows use the [cp1252](https://en.wikipedia.org/wiki/Windows-1252) encoding, Cyrillic versions of Windows use [cp1251](https://en.wikipedia.org/wiki/Windows-1251), and so on. Here is a full reference list of [Windows "Code Pages"](https://en.wikipedia.org/wiki/Windows_code_page), and here is a larger list of [historical encodings](http://unicodebook.readthedocs.io/historical_encodings.html). If you're unable to manually determine the encoding of your file you can attempt a statistical detection with [**Chardet**](https://pypi.python.org/pypi/chardet).

Unicode is a deep topic that's closely tied to the history of computing. If you're interested in a quick practical and historical overview the [Unicode HOWTO in the Python documentation](https://docs.python.org/3/howto/unicode.html) makes for excellent reading.

