---
title: Intro
author: Thinkful
team: grading
time: 45
uuid: f45217a8-bf79-497c-b633-299fb564476e
---

Businesses rely on numbers to guide decision making and to exploit their competitive advantages whenever possible.
As a result, companies have always leveraged state of the art computing technology to understand as much data as possible. Even though it’s a relatively new term, “big data” simply refers to a desire to glean relevant information from the most data. In recent years, as processing power and storage capacity have grown and prices for these services have dropped, businesses have gained the ability to tap massive troves of data.

The sheer amount of data available is staggering, as data generation exponentially expands. In 2013, Science Daily [reported](https://www.sciencedaily.com/releases/2013/05/130522085217.htm) that  90% of all data ever created in history has been generated in the last two years; IBM followed up a year later with a reminder that each year we generate 10 times more data than the prior year. Today, IBM reports that 2.5 quintillion (2.5 x 1018) bytes of data are generated each day. As more devices - particularly internet-of-things devices — come online, and more and more people gain internet access, the data generated daily will only increase.

For a data scientist, the availability of big data is both enticing and daunting. To better comprehend big data, most companies will describe it in the context of the “3 Vs”: volume, velocity, and variety:

* **Volume:** Data comes from a variety of sources, including social media, transaction data, internet-of-things data, and sensor data. Storing this data used to be challenging — even prohibitive — but the availability of distributed storage systems such as Hadoop has reduced this barrier and allowed more data to be stored for longer periods of time.
* **Velocity:** Data often streams into the system at a very high rate, especially when considering point-of-sale transaction data, social media content, and sensor data. Effective utilization of the data requires that it be processed and acted upon in a timely fashion.
* **Variety:** Today, data scientists utilize more unique data types and formats than ever. These include structured data in databases, unstructured text, streaming sensor data, images, audio, stock ticker data, and many others. Big data tools allow data scientists to use varied formats together and identify common signal and information.

## Why does big data matter?

Data is only valuable insofar as you extract insight from it, and the big data side of data science is about bringing your data science skill set to bear on extracting actionable insights from these myriad data sources.  Big data can be analyzed to uncover ways to reduce costs and time, improve product design, make smarter decisions, and answer all sorts of questions. It's behind many state-of-the-art business techniques including:

* cybersecurity
* predicting tool or device failure before it happens
* optimizing delivery routes
* providing personalized offers or recommendations
* real-time language translation

## Who uses big data?

Big data shows up in many industries, but at the forefront — both in terms of data collection and analysis — are finance, education, government, manufacturing, healthcare, and retail. In these domains, big data has transformed business models and provided benefits to both the business and their customers.

As you might imagine, you don’t work with big data on your laptop directly. You need to connect to a larger infrastructure that has been optimized and designed to handle the scale and speed of big data. Typically big data falls into one of three categories: streaming data, social data, or publicly available datasets. When designing a big data project, you should consider storage needs, how much of the data will be analyzed, and how data insights will be put into action.

## Big Data with Spark

So far in your data science education, you’ve focused on the tools provided by Python to build machine learning models. All of the work you’ve done so far has been on datasets hosted on a single machine (often loaded directly into memory); similarly, the code you’ve written has executed on a single system — often in a single process or thread. There is a great deal of power in this approach. In fact, even when working with big data, you’ll often want to explore, build models, and test on samples of the larger dataset. 

Adding big data to your toolkit means that you go from working on a dataset hosted on a single system to working with distributed datasets. The best means to work with distributed, massive datasets is within a distributed computing framework. Distributed computing brings significant challenges — How do you synchronize the code across many processors? What happens if a single processor fails? How do you roll up results when execution concludes?

Apache Spark aims to solve many of these challenges. Spark simplifies the tasks that bedevil developers when working on distributed computing including resource scheduling, job execution, communication between nodes, and so on. Spark was developed from the beginning to work with machine learning algorithms, which means it has been optimized for high-performance in situations where data is accessed multiple times over many iterations.

Spark is the leading open source distributed analytics platform. Its [project page](https://spark.apache.org/powered-by.html) lists almost 100 companies using Spark in production, and there are almost 400 active developers contributing to the codebase on GitHub.

Spark can run in standalone local mode with all processes inside a single Java Virtual Machine, or in standalone cluster mode. Data scientists interact with Spark via APIs in several languages. Spark supports 4 programming languages: Java, Scala, Python, and R. We’ll use Python in our examples for this course.

Spark uses a data representation called the Resilient Distributed Dataset (RDD). This is a data type very similar to the dataframe you know from Pandas but optimized to be distributed across multiple computers, residing in memory across all of them. Once an RDD has been created, by using Spark methods and functions, you interact with this distributed dataset as if it existed only on a single device. As an end developer, you don’t know — or need to know — how the RDD is actually allocated. Spark frees you from those details and allows you to focus on what is important to you — analyzing a dataset.

