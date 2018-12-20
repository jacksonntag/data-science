---
title: Hadoop and Big Data Storage
author: Thinkful
team: grading
time: 45
uuid: 55a0a578-668f-434b-aeba-db6a871197a9
---

So you’re working somewhere with a lot of data, but what tools are you going to need? Chances are they’re going to be using Hadoop.

Here we’ll use Hadoop to refer to the larger environment of Hadoop-based software that is used for storing, moving, and analyzing Big Data under a unified framework. As such there will be several different components we’ll talk about, but it will only be part of the picture. Specifically we’ll focus on the parts that are touched or used for model building and analytics, ignoring much of the infrastructural backend. If you’re going to be building this kind of infrastructure or just want more details about it, check out hadoop’s [webpage](http://hadoop.apache.org/) which lists Hadoop and several associated projects.

## Key Components

Hadoop, sometimes called a Hadoop cluster, has four core components. Two aren’t very interesting from a data science perspective (assuming you’re not maintaining the cluster). Commons is the utilities structure for Hadoop. As a data scientist, a data engineer should typcially be handling the utilities for you. YARN is a scheduling and resourcing tool.

HDFS, or Hadoop distributed file system (there’s that word, ‘distributed’), is where the data in Hadoop actually lives. This is a distributed data store with fast access tools. What this functionally means is that instead of all the data being stored on a single machine and a single drive, it is distributed across many. This has advantages in stability (one machine goes down and the world does not end) and speed of access.

MapReduce, our final component which is actually the basis of the Hadoop project as a whole, is a data processing tool for distributed systems. More likely, a data scientist would use a tool like PIG for pulling raw data from HDFS or other large form data stores, which is functionally the same but with an easier to use interface (more querying based than the original MapReduce). PIG won't look totally unlike SQL, and the challenges of navigating data with it usually has more to do with the internal data model and structures than PIG itself.

## Other Pieces

Though it is important to understand a bit of that aforementioned Hadoop architecture, most of the time a data scientist won’t actually be working with those tools (with the possible exception of Pig, which executes jobs in a language called Pig Latin, no joke). That’s because most of the time the data will be set up with a querying layer. In the case of Hadoop, that is typically Hive (though it could also be something like Presto, and you could accomplish a lot of the same goals with a PIG script).

Querying is a nice, easy way to access huge amounts of data and get only what you want which is then brought to your local machine or kept on a separate server. We covered queries in SQLite as part of the first unit of this course. Hive allows you to use those same tools and structures for large datasets in HDFS. It even has its own SQL-like querying language called HiveQL.

So what are the differences between HiveQL and SQLite?

The first is going to be speed. HiveQL is going to be slow. Part of this is a function of the size of the data set, but it also is just generally pretty slow software. It’s not uncommon for Hive queries to run over the course of hours or even days. Again there are faster tools for accessing data in HDFS, particularly Presto or using other database types (Redshift, Vertica, etc), but these can require more hardware and be generally much more expensive.

Otherwise, the differences are very minor from a user perspective (the distributed nature of working on a distributed dataset being the huge difference from an engineering perspective). Engineers have done a lot of work to make distributed data work feel as similar as possible to local work. There is slightly different syntax around joins (you have to specify if the join is outer using [left and right joins](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Joins)) and datetimes (every SQL language seems to have slight variation around how it uses time).