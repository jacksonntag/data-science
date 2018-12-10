---
title: 'Challenge: sentiment analysis for Amazon reviews'
author: Thinkful
team: grading
time: 60
uuid: b3e17176-a451-4383-9e09-48ce5d04b6f2
---

Now that you've looked at an example of how we can use Spark in batch mode, it's time to try it out on your own.

In this challenge you'll revisit the sentiment analysis we did earlier in the course - specifically, the [Amazon reviews dataset](http://jmcauley.ucsd.edu/data/amazon/). You should choose one of the 5-core datasets. Keep in mind that if the data is g-zipped, you'll need to unpack the dataset before you use it.

You should complete this challenge in a Jupyter notebook, which you'll need to work on within a Docker container. To get your container up and running, you'll use the `docker run` command like before, reusing our pre-built Spark image earlier: `thinkfulstudent/pyspark:2.2.1`. For example, you might run:

```
docker run -d --rm -p 8888:8888 -v /path/to/big-data-student-resources:/home/ds/notebooks thinkfulstudent/pyspark:2.2.1
```

Now, on to the task at hand!

It's always important to start with a clear goal in mind. In this case, we'd like to **determine if we can predict whether a review is positive or negative based on the language in the review.**

We're going to tackle this problem with Spark, so you'll need to apply the principles you've learned thus far in the context of Spark.

Some tips to help you get started:

* Pyspark always needs to point at a running Spark instance. You can do that using a SparkContext.
* We're still working in batch mode, so you'll need to load an entire file into memory in order to run any models you build.
* Spark likes to execute models in a pipeline, so remember that when the time comes to set up your model.
* Spark's machine learning algorithms expect numeric variables.

When you're done, save your notebook and push it up to GitHub. Submit a link to your notebook below.

After submitting your work, review the example solution provided in your big data student resources directory - `examples/Amazon Reviews Exercise.ipynb`.