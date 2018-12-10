---
title: What is a biostatistic?
author: Thinkful
team: grading
time: 45
uuid: a3256a71-5861-4fdc-ad5c-554171419bbb
---

You may be wondering what distinguishes biostatistics from regular statistics.  Many fields use statistical methods (psychology, medicine, demography, even computer science at times) but they don’t call it ‘psychostatistics’ just because the person running the numbers has a Psych Ph.D.  Biostatistics is separate for a number of reasons:

It deals with unique data that have unique requirements.  Modeling factors that predict time until death requires a class of model we haven’t encountered yet: survival analysis. Biostatistics isn’t the only field to use this technique (engineers use it to model time until mechanical failure) but people interested in modeling death were the ones who pioneered it.

Statistical significance does not automatically mean clinical significance.  Biostatisticians are in the unusual position of wanting to run inferential/interpretive models on what can be rather large datasets.  This embarrassment of riches causes trouble because, as you may recall, the signifier of a significant feature in a model is a low p-value, based on the t-value.  The t-value is the ratio of the size of the effect to its standard error, and the standard error gets smaller as sample size goes up.  Which means that for very large samples, even the tiniest effects can be statistically significant-- even if they are clinically (medically) meaningless.  

For example, imagine a study testing a new drug for lowering blood pressure.  The study runs a t-test and finds a statistically significant difference: the new drug lowers BP by an average of 2 points relative to the control.  A biostatistician needs to weigh this finding against the clinical guidelines for blood pressure variability to know whether this makes the drug worth pursuing.

Complex implementations of Bayes’ Rule.  A lot of the time, biostatisticians want to compute the probability of various complex outcomes (developing a disease when a person has characteristics X, Y, and Z).  Computing the unknown distribution of these probabilities is computationally non-trivial, so biostatisticians use a nifty set of algorithms called Markov chain Monte Carlo (MCMC) to short-circuit the problem.  Again, many other fields use MCMC, but it has particular relevance to biostatisticians’ concerns.

## Sources of Biological Data

So if you want to do a Biostatistics project, you need some biological data.  Here are some sources to get you started:

Unsurprisingly, the [Centers for Disease Control and Prevention](https://data.cdc.gov/) have great biological data.  They also offer some analytical support through their [National Center for Health Statistics](https://www.cdc.gov/nchs/).

The [Global Health Observatory](http://www.who.int/gho/en/) of the World Health Organization has health data from hundreds of nations.  It is most easily available from the [Global Health Atlas](http://apps.who.int/globalatlas/).

If you want to focus on survival analysis, the [Human Mortality Database](http://www.mortality.org/) is your friend.  

Clinical trials may sometimes make their data public after publication- even if the file isn’t online, it can sometimes be acquired by directly contacting the corresponding author of the research article.  JAMA, [The Journal of the American Medical Association](http://jamanetwork.com/journals/jama) and its sister journals have some of the best peer-reviewed biostatistical studies out there and are a