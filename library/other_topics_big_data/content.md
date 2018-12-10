---
title: What is big data?
author: Thinkful
team: grading
time: 60
---

So what is big data?

It depends on who you ask. A general rule of thumb though is the more experience someone has working with data and modern techniques, the larger a dataset has to be to qualify as ‘Big Data’.

For some people it’s going to be something that’s too big for Excel. You can’t really look at it in its raw form and learn much. You can’t count the number of rows yourself. From our perspective, and that of people who work with programming languages like Python or R by default, that isn’t an interesting definition.

A far more functional and modern definition is data that is too large to work with on a local machine. This does not count when the database is too large to clone to a local machine, meaning it has too much data to store on your local hard drive as is often the case, but when the data you want to work with from that database is still too large to do so.

So how big is that?

We’re at least talking gigabytes of data. That can be millions of rows. Often we’re getting into terabytes and billions of rows. It can easily push higher than that. If you’re getting into petabytes or exabytes you’re likely working with some really specialized machines. Lucky you, but no chance is that all going to be on your local machine.

## Issues of big data

When data gets that big, several issues start to arise.

Firstly, getting the data itself becomes more complicated. You have massive amounts of data that the simple methods we’ve used previously wouldn’t work. Even single job sql, which is where one processor is searching through the tables to gather your data, is often too slow. Luckily for us there is a whole set of resources to help us get to our data and get it into a usable form. We’ll talk about Hadoop, some of the infrastructure designed for this, in the next assignment. We’re also going to assume that the act of designing a storage system for this falls into data engineering, rather than data science.  Your job as a data scientist is to access, manipulate, analyze and interpret the data once it is stored.  Keep in mind, though, that not everyone distinguishes between data engineering and data science, particularly in smaller companies.

You also have to be able to understand what's going on with that data. This is where visualization and summary statistics will come in handy. We've covered these tools already in the course, but it is worth mentioning that when you're working with truly 'big' data, the way you think about them may change. We've mentioned things outliers before. The difference is, when you're trying to handle millions of billions of observations, those outliers could be thousands or more. 

How you visualize that is something worth considering, though there is no 'right' way. You do, however, have to be aware that as every visualization in some way simplifies or glosses over some data, those counts could be more significant than before. That can have real implications for your analysis. We won't discuss this further in this lesson, but it is an important principle to keep in mind.

Lastly, there is the difficulty of training a model on a massive amount of data. There are huge advantages to using a large amount of data to build models. For some classes of models, particularly neural networks, a large volume of data can be essential to getting meaningful performance. But again, if you can’t bring it all onto your machine what’s a data scientist to do? Or, if it’s too slow to work with it all at once, how can you build a model faster? Again, there is a set of tools designed to deal with that as well. That will be covered in the third assignment of this lesson. 

All of these lessons are only introductions to the tools, giving you the lexicon to port some of your knowledge from previous lessons to this framework. This is a fast evolving sphere of data work that is often very particular to the company or infrastructure you end up working with, so be prepared these threads we are laying here much deeper should your job ultimately involve much of this work.