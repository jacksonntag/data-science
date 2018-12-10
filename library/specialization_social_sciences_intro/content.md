---
title: Intro
author: Thinkful
team: grading
time: 90
uuid: 90d9b2f2-8591-4394-9f97-42fef2e69025
---

The majority of this bootcamp has focused on *prediction*- building models that describe a phenomenon with sufficient accuracy that they can give information about outcomes given known inputs.  In a prediction-focused environment, features are useful because they allow us to build a model, but we aren’t primarily interested in what the features mean in and of themselves. 

The social sciences (psychology, sociology, economics, political science, demography, linguistics, and others) have a different focus.  Social scientists are interested in *processes*- they want to understand how various phenomena (crime, love, election outcomes, etc) work.  For process-focused modeling, the focus is on identifying and interpreting meaningful relationships between the phenomenon of interest and the feature-set.  This leads to different criteria for assessing model quality.  Furthermore, models and techniques that provide rich and interpretable information about features (most types of regression, PCA, clustering) are preferred over models and techniques that do not (neural networks, random forests, boosting).

Social science encompasses any and all phenomena related to society and the relationships of individuals within society.  For the purpose of this module, we’re going to focus on techniques for modeling *change* within persons across time.  Many of the fields that make up the social sciences are interested in understanding and producing change: psychologists want to improve mental health, sociologists want to enrich local communities, political scientists want to understand changes in political opinion across the election cycle, etc.  By following a sample of people over time while repeatedly measuring our variables of interest, we can begin to understand how, when, and even why people and societies change.


## Interpreting parameters


The major difference between predictive and interpretive models is the role of *model assumptions*.  You may recall that, way back in the beginning of the course we talked about situations where the mean of a variable could be deceptive: In a variable with values clustered around 10, an outlier of 100 could shift the mean far away from the true ‘central tendency’ of the data.  This is because when calculating the mean, we *assume* that the values in the variable are evenly distributed around a central cluster.  If the data violates that assumption, the mean statistic may no longer be trustworthy as a measure of central tendency.

Violated assumptions are a major problem if we want to *describe* data, to interpret models with the goal of learning how our various variables relate to one another.  When our goal is interpretation, models work primarily as a ‘summarizing’ tool to reduce the volume of raw data to a smaller set of parameters that our human brains can understand.  A model with violated assumptions will provide an inaccurate representation of the underlying data, leading to incorrect interpretations.

On the other hand, if our goal is *prediction* then model assumptions become less important-as long as our model has an acceptable level of predictive accuracy when cross-validated, we’re happy.  With prediction, what matters is that a model performs well across many different subsets of the data, and isn’t overfit.  A consistently-performing model that stomps all over the underlying statistical assumptions is better for prediction than an assumption-consistent model that only performs well on the training set.  That said, a model based on data that violates assumptions will often have low predictive accuracy, and be rejected on those grounds without the need to explicitly check assumptions.

Take the metaphor of the well-meaning friend whose movie recommendations you always hate. Their internal ‘model’ of your tastes in entertainment is obviously based on some pretty wrong assumptions and is giving them bad data.  On the other hand, because they are *consistently* wrong, their recommendations still allow you to predict whether or not you’ll enjoy a film: If they say you’ll love it, you know you’ll hate it and vice versa.

Different models have different assumptions-make sure to check them out before you get carried away with interpreting your parameters.

## Panel data

> πάντα χωρεῖ καὶ οὐδὲν μένει
>[Everything changes and nothing stands still.]
> –Heraclitus of Ephesus

The social sciences, particularly psychology and sociology, are interested in change-changes in relationships, in personality, in trust, etc.  After all, observing how a system changes is an excellent way to understand how it works.   For example, imagine a romantic relationship proceeding from stability and happiness to a break-up.  If we wanted to understand what makes relationships stable, we could look at what aspects of the relationship changed to lead to the breakup.  Did communication break down, leading to decreased happiness, and less time spent together?  Or did the couple start spending less time together, leading to communication breakdown?  Or did something else happen?  Change can be thought of as a natural experiment. 

To properly study change, we need to administer the same measures repeatedly across a long enough time interval that the change becomes evident.  For observing break-ups in new (less than a month) relationships, a month or two might be enough time for a significant portion of the couples being observed to break up.  If we wanted to observe break-ups in couples that had been together for 20+ years, the observation period might need to be 10 years or more.  

We also need to include enough measurement points to be able to reasonably estimate the timespan of the change.  If we measured the long-term couples twice, 10 years apart, we might find that some of the relationships had ended and many variables had changed, but we wouldn’t get a good sense for which changes drove the breakup.  On the other hand, repeatedly measuring the same participants is costly for us, and demands a lot from the participants.  

### Panel data vs time series

Time series data (discussed in-depth in the Time Series Specialization) and panel data both represent repeated measures from the same object.  The difference comes from the ratio of sample size (N) to number of measures (T).  Traditional time series data follows one object (N=1) with a very large number of measures (T).  National GDP is an excellent example of time series data.  Panel data follows multiple objects but has fewer measurement points.

### Strength of panel data

The best thing about panel data is that each person (or group, or object) being observed serves as its own control.  Contrast this with a traditional t-test that compares two groups.  While random assignment is used to try to get the two groups to be approximately the same in various ways, they won’t be exactly the same, and these irrelevant group differences introduce noise into the analysis.  With panel data, we are comparing a person to themselves at a different measurement point. While many things may have changed for the person between measurement points, many others remain the same, resulting in a less noisy, more sensitive analysis.

### Weakness of panel data

Missing data can be a real problem in a panel design.  Depending on the analysis technique being used, missing data at one measurement point may result in throwing out all the data from that person.  Drop-outs, where a person stops responding to any measurement requests partway through the study, are a particularly serious form of missing data, since their reasons for dropping out may be linked to the outcome under study.  

Solutions for missingness include:
* Carry it forward: the missing datapoint is replaced by the value from the previous timepoint.  
* Fill in the person’s mean
* More complex imputation
* Using methods that allow missing datapoints
* (for drop-outs) creating an indicator variable to include in analyses that says if or when a person dropped out

### Working with panel data

The trick with panel data is that any model needs to include a parameter that links multiple observations from the same person together.  Without this parameter, the model will treat all observations as independent, resulting in incorrect error estimates.  In addition, as with time series data, it can be useful to explicitly model time-based dependencies.  For example, responses at consecutive measurement points are likely to be more similar to one another than they are to responses to more distant measurement points.  

For panel data with a particularly low T (say, 3 to 4 measurement points), modeling time-based dependencies should be avoided as it increases the likelihood of overfitting.

### Panel Data Terminology Note

What we call ‘panel data’ is also sometimes called ‘longitudinal data’ if the time period over which the measurements are taken is of interest.  There is also *cross-sectional* panel data.  This data is collected at one timepoint only but meant to simulate the passage of time by selecting groups that are in different stages of the process under study.  For example, a study on aging in mid-life adults could either follow a sample of 35 year olds for 20 years (longitudinal data) or could collect data from groups that were 35, 45, and 55 years old (cross-sectional panel data).  Cross-sectional panel data is sometimes necessary when a longitudinal study would be prohibitively expensive or slow.  However, because a cross-sectional approach conflates the passage of time (aging) with societal changes across decades, it is often criticized.  

## Data sources

Panel data can be more ‘expensive’ than other forms of data because it requires a) repeatedly administering the same measurements, b) a framework for linking each person’s data at each timepoint with their data from other timepoints, and c) keeping respondents motivated to continue completing measures over time.  To wring out as much value as possible from the data, some of the larger panel datasets have been made publicly available.  Here is a list of repositories for some very exciting panel data. This page may be useful to refer back to should you wish to create a social-science-focused capstone.

### MIDUS

[Midlife in the United States: A National Longitudinal Study of Health and Well-Being](http://midus.wisc.edu/), or MIDUS, represents a rich pool of measures of all sorts of psychological and physical health information collected repeatedly in each of the last three decades.  In addition to the surveys, at each timepoint a subset of people also completed an 8-day daily diary study looking at their responses to the stresses of the day.  This means that, from a repeated measures perspective, there are a *lot* of surveys with three timepoints, separated by a decade.  In addition, within each decade there is data from eight consecutive days of stress assessments, for a total of 24 timepoints (with 8 at one-day intervals, then a 10-year interval, then 8 more, another 10 year interval, and then the final 8).

### WHO

For social scientists studying factors affecting health, the [_World Health Organization Global Health Observatory_](http://apps.who.int/gho/data/node.home) is a treasure trove of data spanning many countries.  Because the data describes countries, rather than individuals, analyses can focus on how different countries change at different rates and in response to different factors.  For example, the WHO has estimates for the number of people living with HIV in over 200 countries, collected in 2000, 2005, 2010, and 2015.  

### Centre for Longitudinal Studies

The Economic and Social Research Council of the UK has several cohort studies (following a group of people over a long period of time) available at the [Centre for Longitudinal Studies](http://www.cls.ioe.ac.uk/).

### National Social Surveys

Many countries now administer Social Surveys on a regular basis.  These surveys target attitudes, behavior, social change within the nation.  The [American General Social Survey](http://gss.norc.org/) (GSS) and the [International Social Survey Programme](http://www.issp.org/menu-top/home/) share some questions, which is helpful for cross-national comparisons.

### Experimental Data

Of the social sciences, psychology has the strongest focus on understanding what is happening within the mind of individual people.  This focus often necessitates designing experiments to get at very specific phenomena that aren’t accessible through self-reported data.  Some of these specialized experimental datasets are publicly available through the [The Journal of Open Psychological Data](http://openpsychologydata.metajnl.com/) or the [Open Science Framework](https://osf.io/activity/#popularPublicProjects).  More and more scientific journals have begun to encourage authors to make the data supporting their publications available.  For example, [Psychological Science](http://journals.sagepub.com/toc/pssa/current) offers badges indicating whether an article is accompanied by data.  These datasets are often smaller than a data scientist is used to, but quite unique.  

