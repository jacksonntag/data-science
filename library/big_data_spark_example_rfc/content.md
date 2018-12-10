---
title: 'Guided example: big data, Spark, RFC'
author: Thinkful
team: grading
time: 90
uuid: c5d103b6-1aa4-4232-aa08-d8693db1ede4
---

In this assignment, you'll create your first model with Spark. We'll walk through building a random forest classifier, using the UCI HAR (human activity recognition) dataset, which contains data captured by smartphones as test subjects did different activities like walking, sitting, and laying down. 

## Setup

In the previous assignment, you cloned [this GitHub repo](https://github.com/Thinkful-Ed/big-data-student-resources), which contains the Jupyter notebooks and datasets that you'll need for this assignment, and future walkthroughs. Begin by reading through the material in the curriculum for each walkthrough, and then move on to run the appropriate notebook locally. 

To get started, recall that you'll need to use the `docker run` command from the previous assignment. Be sure to replace `/path/to/big-data-student-resources` with the correct local path to the repo you cloned.

    ```
     docker run -d --rm -p 8888:8888 -v /path/to/big-data-student-resources:/home/ds/notebooks thinkfulstudent/pyspark:2.2.1
    ```

Now open Jupyter notebooks in your browser by going to localhost:8888. From there, open the `RFC with Spark in Batch Mode.ipynb` notebook. After reading the background information below, work through the guided example in this notebook.


### Working with Spark in batch mode


We'll begin our machine learning with Spark exercise by using it in __batch mode__. This mode is most similar to the approach you've taken so far in this course: load a dataset, clean it, then run models and evaluate their performance.

Spark's other mode — _streaming mode_ — differs from batch mode in that, under streaming mode, you do not have access to all of the data. Instead, you ingest data into Spark over a period of time. As each data element arrives, you perform data science tasks (clean, classify, etc) on the new data, then archive the result. Don't worry about the details of this now - we'll cover it soon enough. For now, you only need to be aware that there are two modes we can work from in Spark.

Spark works a little differently than the data science stack you've worked with so far. In the data science stack, you are writing Python code that executes immediately on your local device.

Spark, on the other hand, lives outside the Python environment. We pass instructions to the Spark server, Spark performs the requested calculations and reports back to our notebook. This server paradigm allows us to create and test models locally, and then once we're ready to deploy to production, we simply point our Python code to a remote server that is configured to handle larger data sets.

Spark uses the concept of a __pipeline__ in which we configure a number of steps that only get executed when we tell the server to run. This pipeline approach allows us to configure models and run them through multiple steps more efficiently on big data.

It's always a good idea to review the documentation for modules, methods, and functions we'll use. Everything we look at here can be found in the Apache Spark documentation. You don't need to read the documentation in depth now, but you should refer to it when you come across a piece of code you're not familiar with, or when you're unsure how to proceed in a challenge.

In particular, you should familiarize yourself with the:

* [Spark Overview](https://spark.apache.org/docs/2.1.0/index.html)
* [Python API Documentation](https://spark.apache.org/docs/2.1.0/api/python/index.html)

For our work in this assignment, it's also good to read about random forests in Spark [here](https://spark.apache.org/docs/2.1.0/ml-classification-regression.html#random-forests). 

#### Background: the UCI HAR dataset

The dataset for this assignment contains data from experiments on 30 subjects who wore a smartphone attached to their waist. They performed 6 activities:

* walking
* walking up stairs
* walking down stairs
* sitting
* standing
* lying down

The activities were recorded with video, which enabled time-stamped correlation with motion values collected from the smartphones. In particular, 3-axial linear acceleration and 3-axial angular velocity were captured from the device's accelerometer and gyroscope. This resulted in a 561-value feature vector, plus its corresponding activity label.

As you'll see in a moment when you go through the `RFC with Spark in Batch Mode` notebook, our data for this exercise is in a file called `allData.csv`. This file contains the same data as the original UCI HAR dataset (available [here]((https://archive.ics.uci.edu/ml/datasets/human+activity+recognition+using+smartphones)) but cleaned up so it's ready to use in Spark.

The original dataset is comprised of four files. There is training data, which contains one file for features and one for labels, and test data, which also contains one file for features and one for labels. 
    
Here's what we did to clean up the original data:

1. The original source files are space-delimited and unfortunately, there is inconsistency in spacing. Most of the time a single space is used to delimit, but in some places, there are double spaces. If we were to import the original data with these inconsistencies, breaking on spaces, these double spaces would lead to extraneous columns and create problems for our classifier. Therefore, we removed all double delimiters and replaced spaces with commas. This second step was not absolutely necessary, but we prefer to use the more common CSV format.

2. We merged the test and training feature data into a single final dataset. The labels are the same for both training and test data, so we created a single label file (`activity_labels.csv`).
 
As you'll see in a moment, the final dataset ends up having  __10,299__ rows and __562__ columns. All values are numeric. The labels are integers, and the features are doubles. Because the source data is already numeric, it's simpler to build and demonstrate our classifier in Spark.

## Try it out

With that context, you're ready to work through the walkthrough. Open the `RFC with Spark in Batch Mode` notebook in your browser, and closely read through it, executing each cell. At the end of the walkthrough, you'll find some suggestions for further exploration you can do on your own.
