---
title: Dealing with missing data
author: Thinkful
team: grading
time: 60
uuid: c99f998a-758f-458c-8026-aef90c34103e
---

In checkpoint lesson we'll  introduce you to the different concepts of missingness, and give a brief introduction to how to impute (replace) missing data.

## Dropping missing data

Some datasets may be perfectly complete, but many will arrive with some missing values. Cleaning can increase the amount of missing data. Even if missingness is random, it can cause difficulties for analysis. The Python implementations of basic statistical methods like ANOVA, t-tests, and correlations will fail if any of the variables involved has a missing value.

One way to solve this problem is to drop any rows that contain missing values in your variables of interest. The pandas package has the `.dropna()` [data frame method](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.dropna.html) for doing exactly this:

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/065dc48354"></iframe>


## When Does Missingness Matter?

Sometimes dropping all rows with missing data is fine, but sometimes it creates problems. Missing data matter if we believe the missingness will cause:

 1. Loss of statistical power because so many rows have to be thrown out, making it harder to detect effects, or
 2. Bias because certain values are more likely to be missing than others.

To know when to worry about missing data and when to throw out incomplete cases and proceed as planned, see where the missingness falls in the following categories:

**Missing Completely at Random** ("MCAR"):
 1. A catastrophic flood washed away some of the servers and 20% of the data was lost.
 2. Unless so much data is lost that sample sizes are now too small, it is fair to throw out the missing values and proceed.

**Missing at Random** ("MAR")

 1. Women are more likely to skip a question about weight, regardless of their actual weight.
 2. Because we can explain why the data is missing using data we have, we can proceed as long as we include the variable that "explains" the missingness in our analyses.
 3. There is no way to know that data is MAR, but sometimes we can assume it is.  If we find a variable in our dataset that seems to differentiate really well between missing and non-missing (90% of the people with missing values on the "depression" score are men) we have reason to suspect MAR.

**Missing Not at Random** ("MNAR")
 1. LGBT individuals less likely to answer a survey question about their sexual orientation.
 2. Systematic missingness: People who would answer in a certain way (LGBT vs. Heterosexual) are less likely to answer at all.  
 3. Stop, do not pass Go, do not collect $200.  If we throw out MNAR data, we end up with a biased sample (proportionately fewer LGBT people than in the population we want to study) and biased conclusions.
 4. Note that since, by definition, we don't know what people would have said for questions they don't answer, MNAR is an assumption based on looking at the data and noticing what *isn't* there: Abnormally low counts of LGBT people, almost no men who say they are depressed, variables with missingness where nobody picks the highest or lowest value, etc.

What do you do if you have MNAR data you can't drop (or if it is MCAR or MAR but dropping missing values leaves your sample too small)?


## Imputing Data

In cases where we want to keep all the information from all rows, even incomplete ones, we can "guess" what the missing data would have been and fill in that cell with our guess.  This approach is called **imputation**.

There are many methods for imputing data, from the simple to the very complex.  The most straightforward involves replacing missing values with the mode, mean, or median of the variable.  This method isn't perfect: it keeps central tendency the same, but reduces variance and correlations among variables.  Here's how it works:

<iframe height="600px" width="100%" src="https://trinket.io/embed/python3/bb3980131e"></iframe>

If you'd like to see a more sophisticated method of replacing missing data, involving grouping existing entries into "similar" groups and filling in the missing values within a group with the mean for that group, check out this [in-depth tutorial](https://www.analyticsvidhya.com/blog/2014/09/data-munging-python-using-pandas-baby-steps-python/).

## Beyond Imputation

If the causes of MNAR (or of major, catastrophic amounts of missingness that is MCAR or MAR) are clear and easy to fix, then fixing those causes and collecting new data may be easier than imputation.  Either run the study afresh, or collect more data with an intentional focus on the groups with highest missingness.  For example, if a coding error in a tech usage survey means data wasn't recorded for any Mac users, it may be easier to fix the coding error and run the study again (or fix the coding error and collect data from just Mac users) than try to impute such a centrally important variable.