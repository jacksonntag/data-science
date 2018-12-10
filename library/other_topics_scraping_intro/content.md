---
title: "What is scraping?"
author: Thinkful
team: grading
time: 30
---

Web scraping (or data scraping) is the process of programmatically extracting data from a website and saving it to a file or database. Writing a scraper, collecting some data, and then doing some basic analyses on the data is a popular way for a data scientist to build their online portfolio: you’re guaranteed a unique dataset and can achieve an impressive-looking presentation with a few plots and basic statistics.

Despite its surface sexiness, however, a knowledgeable recruiter is unlikely to be awed by scraping skills alone. In the vast majority of cases, companies hire data scientists because they already have *too much* data, and need someone to do in-depth analyses to make sense of it. In addition, as more and more websites offer APIs (_Application Programming Interfaces_, something we will discuss later on), basic scraping is becoming less necessary for data retrieval.  And as you are no doubt aware by now, the web is full of [data you can analyze](https://github.com/Thinkful-Ed/data-201-resources/blob/master/data-sources.md) right away, no scraping required.

That said, there are times when scraping will come in handy. Sometimes websites have information that is unique, of special interest, and that can’t be accessed in any other way. In this module, you’ll learn how to write a basic web scraper that will navigate a website and retrieve specific information from its pages. You’ll also learn about the netiquette of scraping and some basic do’s and don’t's.  

## What is scraping?

From a high level, web scraping is pretty simple. To scrape, you need to be able to:

* Access web pages
* Locate specific information in those webpages
* Save the information you located somewhere else to be accessed later

## Accessing web pages

You’re probably used to using your web browser to access webpages. To programmatically access the content of a webpage, we skip the browser and send a **request** to the web server directly using the URL for the web page we want. The server you send will send back a **response**.  This response will include either the HTML code for the web page you requested, or, if something went wrong, an error code.

Many web pages are accessible to the public, but some require authorization. Think about how a page like [https://twitter.com/](https://twitter.com/) or [https://mail.google.com](https://mail.google.com/mail) looks different depending on whether you’re logged in. When requesting web pages that require authorization you need to include that data (passwords, cookies, tokens, etc) with the request you send.

## Locate specific information in each page

Once you have the response, you’ll need to **parse** what's returned to pull out the specific information that you want.  Usually, the HTML contains certain consistent markers or clues that define the page and make it easier to find the information you’re looking for without having to read each page manually. There are various parsing languages and Python libraries you can use to make parsing HTML easier.  We’ll be using [Xpath](https://en.wikipedia.org/wiki/XPath) expressions.

## Save the information somewhere

Since scraping is most useful when we want to gather lots of information, storage is an important consideration. The results of scraping can be stored in various file formats, from simple csv or json to direct dumping into an SQL database. To work with the data later, you load it from the file. This is different from our usual procedure of keeping data in the Python working environment at all times.

## Tools

There are Python libraries that will cover each of these steps separately. For example, we could use the [Requests](http://docs.python-requests.org/en/master/) library to access the web pages, the [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/) or [lxml](http://lxml.de/) libraries to parse the pages, and the [json](https://docs.python.org/3/library/json.html) module or [pymysql](https://github.com/PyMySQL/PyMySQL) library to store the info.

Instead of these, however, we’ll be using [scrapy](https://scrapy.org/), a one-stop-shop Python library and API that integrates all three steps.  Why?  

## Things Get Messy

In a perfect world, we know that all the webpages we want to scrape will be formatted the same, that the information we want will be on every webpage we go to, and that information will have a consistent and known format. In that world, a piecewise scraping strategy using the libraries listed above will work fine.

In real life, sometimes web pages are inconsistently formatted so that the parsing syntax we wrote for one fails on the other.  Information that is available on one webpage will be missing from the next. A parsing query that returns one item 99% of the time may return 100 items the other 1% of the time.  Queries may return poorly-formatted data.  Servers may crash or reject our requests.  All sorts of things can happen to derail a scraper, which would lead to bad data getting into our database or the process halting altogether. 

When the unexpected happens, we want the scraper to pick itself up and keep going to the next request.  Scrapy is excellent for this – it has built-in default methods to keep it from crashing on the first unexpected input or failed request. For very small projects involving only one webpage, scrapy may be overkill, but most of the time this robust framework will get you where you want to go. It’s better to cut a plank of wood with a chainsaw than try to chop down a tree with a handsaw.

