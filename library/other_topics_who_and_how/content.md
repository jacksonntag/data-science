---
title: Who and how?
author: Thinkful
team: grading
time: 45
uuid: dd466780-ed7b-4a89-879b-d60e1099ed1a
---

At the same time as you put together your questions, you need to consider *who* you want to learn about, and *how* you’ll administer the survey.

## Weights

It is a frustrating fact in survey research that some demographic groups are more likely to complete surveys than others.  One way to overcome this problem is by using weights.  Weights work by causing the demographics of your sample, and the frequency of their respective responses, to match the demographics of the population you want to understand.  

For example, imagine you are studying customers in Baltimore, a city with a population made up of (as of the 2010 Census) 63% African Americans, 28% Whites, and 2% Asians, with smaller percentages of other groups.  Yet your sample has the following demographic split:

|                  | Baltimore | Sample | 
|------------------|-----------|--------|
| African-American | 63        | 50     |   
| White            | 28        | 40     |       
| Asian            | 2         | 1      |   

While this may not be a problem if you want to study each demographic group separately, the statistics for the whole sample will be biased by the overrepresentation of whites relative to Baltimore as a whole.  If whites respond differently to your survey questions than African-Americans and Asians do, then your survey results won’t accurately reflect the people of Baltimore.

To fix this, you can apply weights so that each survey response provided by a white person is weighted *less* and each survey response provided by African Americans or Asians is weighted *more*.  To get your sample to match the area’s demographics, compute weights by dividing the true population percentage by your sample percentage:

|                  | Baltimore | Sample | Weights |
|------------------|-----------|--------|---------|
| African-American | 63        | 50     | 1.26    |
| White            | 28        | 40     | .7      |
| Asian            | 2         | 1      | 2       |

Basically, you are acting as though the data from each of your African American respondents represents 1.26 African Americans in Baltimore, while the data from each of your white respondents represents .7 whites in Baltimore.  Because Asians are seriously underrepresented in your sample, each Asian person’s data is standing in for two Asians in Baltimore.

This weighting technique is used by major polling companies such as Gallup-- each company has their own particular weighting scheme.  Weights can be based on any slices of demographics you can define, from the very broad (like race) to very narrow (different weights for African-American women under 30, Hispanic men over 55, etc).  Of course, the narrower your slices get, the more vulnerable you are to bias if the people you weigh heavily aren’t representative of their demographic group.  For an extreme example of finely-sliced demographics groups and their consequences for results, check out [How One 19-Year-Old Illinois Man Is Distorting National Polling Averages](https://www.nytimes.com/2016/10/13/upshot/how-one-19-year-old-illinois-man-is-distorting-national-polling-averages.html?_r=0) from the New York Times 2016 election coverage.   

## Power 
Bigger samples lead to more precise estimates and the ability to detect smaller effects.  An **effect** can be defined as the ratio of the size of your parameter of interest to the variance in the parameter estimate.  For example, if you want to compare the ages of employees at two different company locations, your parameter of interest is the difference in ages, and your variance estimate is the pooled variance of the ages at the two locations.  An effect size of 1 would imply that you are interested in seeing if the age difference between the two groups is as large or larger than the pooled variance.  

Your ability to detect an effect in your data is known as **statistical power**.  Why do larger samples have more power?

Imagine you have a population with a true mean age of 40.  You don’t know this mean yourself, and set out to discover it by taking a random sample of 5 people from the population and calculating the mean age of the sample.  You get ages 54, 35, 48, 32 and 102 for a mean age of 54.  Uh oh… Old Man River is going to be a problem.

You sample another 5 people (41, 64, 29, 45, 33) and compute the mean for all 10 together: 48.  Still not great, but better.  You sample another 10 people- that sample has no weird outliers, and its mean age for those is 38.  Your overall sample mean for 20 people is now 43, much closer to the true mean.

The point here is that the bigger your sample is, the less influence any one observation will have on your analysis-- and therefore the more your statistics will resemble the true population.  If you’re having trouble picturing the relationship between sample size and power, check out [the figures here](https://www.statisticsdonewrong.com/power.html).

As another way to express this, you may recall from basic statistics that estimates of variance (noise) in the sample are scaled by sample size.  For example, the standard error of the sample mean is the standard deviation divided by the sample size.  So a bigger sample size means a smaller standard error because they are less affected by noise.

For survey design, the amount of statistical power you want depends on the questions you are asking.  Statistical power is a balance of three things:
The size of your parameter of interest in the population. $\mu$
The amount of variance in your population (the standard deviation).  $\sigma$
The sample size. (N)

$$Power = \dfrac{ \mu}{\sigma/N}$$

Notice the trick here?  Items 1 and 2 depend on knowledge of the mean and variance *of the population*-- yet if you knew the mean and variance of the population, you wouldn’t need to do the survey!  One and two are therefore typically guesses based on previous surveys or domain knowledge.  

Ideally you will collect the smallest N that gives you the power you need to detect your effect.  Less and you miss the effect, more and it’s a waste of resources and participant time.

## Question and response option order

Continuing our flashback to basic statistics, you may recall that random assignment to groups is an important method for getting rid of extraneous factors that we don’t want affecting an experiment.  Random assignment helps us to create two (or more) groups with similar proportions of men and women, similar ages, similar IQs, etc by making it equally likely that any participant will be assigned to either of the two groups.

Randomization is also important when it comes to survey questions.  The order that questions are asked can have an influence on how people answer.  For one thing, questions later in the survey are more likely to be skipped as people get bored or tired, especially in a longer survey.  For another, the act of answering an earlier question may affect later answers.  For example, a [set of experiments in social psychology](http://homepages.se.edu/cvonbergen/files/2013/01/Stereotype-Suscetability_Identity-Salience-and-Shifts-in-Quantitative-Performance.pdf) demonstrated that asking women their gender before giving them a math test led to lower scores on the math test relative to when they were asked about their gender after the test.

The easiest way to resolve order problems is to show questions in a randomized order so that every question has an equal chance of being asked first, second, third, etc each time the survey is administered.  Obviously this won’t work if you are using pencil and paper surveys.  When randomizing, some questions have dependencies (‘Do you have a dog?’  ‘if yes, how much do you feed your dog?’) that mean they need to occur in a certain order; you can also organize questions into blocks and randomize the order of the blocks.

When questions have multiple response options (multiple choice, constant sum, ranking), the item shown first is typically more likely to be chosen than others.  This can be fixed by showing answer options in randomized order.  Other order effects include a preference for options or text shown on the left-hand side of the paper or screen (for languages where people read left-to-right).

