---
title: Spark streaming with network traffic data
author: Thinkful
team: grading
time: 120
uuid: 06b626c9-cf98-48af-90c2-a2b77e8dd1fa
---

Now that we have worked through some examples with batch data, it's time to turn our attention to Spark's Structured Streaming. Our end goal today is to stream and process data in real time with Spark. There are a ton of streaming data sources out there (think Twitter streaming, Citibike data, NYC MTA train arrivals, and so on). Those are all excellent data sources, and you'll get an opportunity to work with Twitter's stream in the next assignment.
​
But as you're first learning about streaming, there's a problem with using real time data — namely, how can we **really** know that we've got our data right? What we need is a static baseline to compare our streaming analysis against to ensure that we get what is arguably the hardest part of streaming right: properly formatting incoming data and ensuring data integrity.

To that end, we actually won't do much heavy lifting on the machine learning side of things. Our analysis will be relatively simple. We'll explore streaming data by working with a small subset of the Los Alamos National Lab network dataset, which contains data about Internet traffic. First we'll do a static analysis of this data to get a baseline result, and then you'll re-run the analysis by streaming that same data locally. This will prepare you for working with real time streaming data in the next assignment.

Like with the introduction to batch processing, we'll give you the background context you need about the data and approach here in the curriculum app, and then you'll go through a walkthrough in a Jupyter notebook we provide in your big data student resources directory.

## Background on streaming
​
Before you start, it's a good idea to read through the following articles:

* [Structured Streaming in Apache Spark](https://databricks.com/blog/2016/07/28/structured-streaming-in-apache-spark.html)
* [Spark Streaming Programming Guide](https://spark.apache.org/docs/latest/streaming-programming-guide.html)

These resources will give you a sense of how one can use streaming - where we can see an advantage, as well as some of the challenges we'll face.
​
Make no mistake, either —— streaming can be hard to get right. In fact, we'll warn you up front that this walkthrough is challenging. But, it's worth it!
​

## The Los Alamos National Lab network dataset
​
Los Alamos has posted a huge amount of network data online in CSV files (available [here](https://csr.lanl.gov/data/2017.html)). For the purposes of this walk-through, the original data set was WAY too large. To make things manageable, we took a small subset of the data - only about 2.5 minutes worth, comprising around 500,000 flows — and split it up into a series of 50 JSON files because JSON is the most common format for streaming data. This will allow us to simulate streaming real time data by treating each of the 50 JSON files as a separate stream object.
​
Each entry in the dataset represents a "conversation" between 2 computers. For each entry, the following fields are captured:

* Time: the start time of the conversation (in a proprietary timestamp format)
* Duration: the length of the conversation (in seconds)
* SrcDevice: name of the device that initiated the conversation
* DstDevice: name of the device that was requested
* Protocol: network protocol used (TCP, UDP, etc)
* SrcPort: network port (0-65,536) on the originating device
* DstPort: network port (0-65,536) on the destination device
* SrcPackets: network packet count sent from the source to the destination
* DstPackets: network packet count sent from the destination to the source
* SrcBytes: byte count sent from the source to the destination
* DstBytes: byte count sent from the destination to the source
​
As you can see, there's a lot here. However, we'll try to answer a relatively simple question:
**From this data, how many web servers can be identified?**
​

## Identifying web servers

To answer our research question, we'll use some basic knowledge about network behavior.  Web servers typically communicate on one of two ports: **80 or 443**. So, if a computer requests one of those ports as the `dstPort` in a flow, it's likely that the destination device (`dstDevice`) is a web server. If we see that computer name come up repeatedly in our request list, then there's a good chance that device is a web server.
​
So for our streaming exercise, we need to build a count query that processes streams as they come in and updates the count of web servers, then reports back to us what it sees.
​
## Do the walkthrough

With that background out of the way, it's time to work through the `Spark streaming` notebook. As in the batch processing walkthrough before, you'll need to run the `thinkfulstudent/pyspark:2.2.1` Docker container. Assuming your container is not already running, use the following command, substituting in the correct path to your big data student resources directory for the `/path/to/big-data-student-resources` part:

```
docker run -d --rm -p 8888:8888 -v /path/to/big-data-student-resources:/home/ds/notebooks thinkfulstudent/pyspark:2.2.1
```

Once the container is running, open Jupyter notebooks in your browser by going to localhost:8888. From there, open the `Spark streaming.` notebook and work through it.

