---
title: Evaluating data sources
author: Thinkful
team: grading
time: 60
uuid: 985d68e8-bb41-4773-8ba8-57fc62abba6a
---

Not all data sources are created equal. It is tempting to look at a dataset and assume it is correct, or representative, or that because it's about the subject you're interested in it can answer the questions you have about the topic. That is not necessarily the case. Evaluating data both for quality and bias is an important skill of data science.


## Bias

We've mentioned the notion of samples versus populations before. It is very common to look at a problem and not be able to get data on every relevant individual, so we take a sample. Whenever we're dealing with a sample, it is essential to ask if that sample is truly random. If you do the sampling yourself, that process can be pretty easy. You know the process you engaged in to sample from the population and you can thoroughly evaluate its credibility.

For example, if you wanted information about the popular kinds of cereal, you could go to your local grocery and make a list of the cereals that they have on the shelf. This will give you a dataset, but not a great one. It's a single sample, biased by things like geographic location. The same principle applies when scraping a website, it's a single sample with the biases associated with that website.

This process becomes much more difficult, however, when dealing with data collected by someone else, and particularly datasets available on the internet. Pay close attention to the method used to collect the data and evaluate what if any biases may be present because of that.


## Quality

It's important when approaching a new data source to try to judge its objective quality. Are there are a lot of unexplained blanks? Is it unevenly distributed across time? Does the volume fluctuate seemingly without cause? All of these things, and many more, can be signals that the quality of the dataset is questionable. Engaging in this questioning early and explicitly will help prevent situations where the conclusions of your analysis are compromised or when poor data quality becomes your conclusion.


## Exceptional Circumstance

What was the situation under which data was collected? This can greatly impact the data and therefore the quality of conclusions you can draw from it. Returning to the grocery example, if you were trying to analyze the eating habits of Americans, you could look at the shopping behaviors at grocery stores across the country. Let's say you obtained a large sample that accurately covered the whole of the country with data from a variety of cities and neighborhoods.

But what if that data was collected on the day before the Super Bowl? Your dataset would then be skewed because the data was collected in  an exceptional circumstance. The shopping behaviors on that day are possibly quite different from normal. Thinking about that aspect of the dataset can again help catch its limitations early on in the process.


## What to do?

So what can you do with data that has issues with its quality or source? There are many options.

Firstly if you can quantify the bias, you can **adjust** to it. For example, let's say you were interested in fishing numbers, but only had data from San Francisco for the given year. You can look at other databases and figure out how other cities typically compare to where you have your data and try to impute larger trends. We'll cover imputing data in more detail later in the bootcamp.

You can also **limit your conclusions** to the scope of the data. Be very clear about where your conclusions are applicable. If you scraped a single online retailer, understand and state that your conclusions only apply to that store. When using data from Amazon, you're talking about Amazon shopping behaviors, not retail consumption as a whole. That analysis can still be highly valuable.


## Drill

In each of the scenarios, find possible shortcomings of the theoretical or actual data sources to answer the given question. What could be done to either adjust the analysis or reframe the question so that you can answer it accurately?

* **Data Source**: Amsterdam availability data scraped from AirBnB on December 24th. **Question**: What are the popular neighborhoods in Amsterdam?

* **Data Source**: Mental health services use on September 12, 2001 in San Francisco, CA and New York City, NY.  Question: How do patterns of mental health service use vary between cities?

* **Data Source**: [Armenian Pub Survey](https://www.kaggle.com/erikhambardzumyan/pubs). **Question**:  What are the most common reasons Armenians visit local pubs?

Write up your answers and submit a link below.

After trying it yourself, you can find a solution [here](https://github.com/Thinkful-Ed/data-201-resources/blob/master/solutions/Prep%20course/3.2.7.md).

