---
title: Survival analysis
author: Thinkful
team: grading
time: 60
uuid: 1d735553-c1c5-4baf-a738-abc24cae3085
---

When it comes to modeling, ‘time’ is a compelling but complex concept.  One way of modeling time is to estimate how much time will pass before an event occurs: death, marriage, hard-drive failure, or what have you.  Modeling time-to-event data is called ‘survival’ analysis, because the methods used were initially developed to create the actuarial tables used by insurers to predict risk of death in potential insurees.

## Issues to Consider when Using Time-to-Event Data

### Defining Time
When analyzing data from clinical trials, a biostatistician may want to predict how long it takes before patients in a drug trial go into remission (no longer show clinically significant symptoms of a disease) after starting to take the drug or the placebo pill.  In this situation, the ‘starting time’ is the date the study begins, and is the same for all participants.  Time-to-event would be days from the start of the study to when a participant enters remission.

Other biostatistical models concern mortality, that is, the age at which people die.  For these data, the ‘starting time’ is each person’s date of birth, and will therefore vary from person to person.  Time-to-event would be calculated by subtracting the date of birth from the day of death.

### Censoring
What if the ‘event’ never occurs?  Or occurs outside of our window of observation?  It isn’t plausible to set ‘time-to-event’ to infinity or to zero in those situations.  Instead, the value of the time-to-event variable is set to the maximum observable value.  A second, ‘status’ variable is used to indicate whether the event happened at all.  This is called **right censored** data: If the event never happened, all we know is that the time to event is greater than the maximum observable value.

There is also *left censored* data, where the starting time occurs before the window of observation begins.  With left-censored data, it isn’t possible to calculate time-to-event *if the event happens during the observation window*.  For example, imagine a drug trial where participants can start taking their drug dosage anytime within a one-month period. Some start at the beginning of the month, and some start near the end.  What is the ‘time to event’ for someone who goes into remission on October 2nd?  Without the starting date, we do not know.

On the other hand, we can still analyze left-censored data if the event *has not yet happened* by the end of the observation period.  In that case, we would treat the case as right-censored, setting the time-to-event value to the length of the observation period and the status to ‘event did not happen’.

### Truncation
With censored data, we know *something* about the time-to-event (usually that it is greater than the size of the observation window), but we don’t know the exact value.  With truncated data, we have no information at all, usually because we’ve chosen to throw out the case during our data cleaning process.  We may choose to truncate left-censored data by throwing out the case if it isn’t possible to estimate the time to event.

Truncation and censoring are often confused.  Just keep in mind, censoring means you have a ‘guess’ at the value (as when body parts are blurred or pixelated when certain scenes are shown on TV), whereas with truncation you know nothing (as when whole scenes are removed entirely).

## Survival and Hazard functions

There are many different survival analysis techniques, but almost all of them are based on the Hazard function, which is closely related to the simpler Survival function.  It isn’t necessary to have the formulas memorized, but do take a glance at them:

The Survival function:  <img class="latex-image" src="https://latex.codecogs.com/gif.latex?$S(t) = P(T > t)$" />
$t$ is the timepoint and $T$ is the time of the event.  So $S(t)$ is the probability that the time until the event $T$ is greater than the value of timepoint $t$.

The Hazard function: <img class="latex-image" src="https://latex.codecogs.com/gif.latex?$\lambda(t) = \lim_{\delta t \rightarrow 0} \dfrac{\Pr(t \leq T < t + \delta t \ | \ T > t)}{\delta t}$" />
Where $t$ is still the timepoint, and $\delta t$ is the one-unit change in time.  The probability here is the conditional probability that the event will occur in the interval between $t$ and $t + \delta t$, given that it hasn’t occurred by time $t$.  The size of the $\delta t$ defines the interval- larger $\delta t$ values will lead to higher probabilities of the event occurring during the interval.

## Cox Proportional Hazards Model

One of the most common models for time-to-event data is the Cox Proportional Hazards model.  This model bears many similarities to logistic regression. It estimates the conditional probability of the event occurring during a given interval, and gives information about how other features in the data (age, gender, etc) affect that probability.

<img class="latex-image" src="https://latex.codecogs.com/gif.latex?$\lambda(t|x) = \lambda(t)\exp(\alpha + \betax) $" />

The ‘Hazards’ in the model name indicates that it is based on the Hazard function ($\lambda(t)$), which you can see in the model equation.

The rest of the equation may look familiar, because it is the standard regression formula.  However, instead of a linear relationship between the outcome $\lambda(t|x)$ and the regression, the regression is used to parametrically modulate the values of the hazard function.  This gives us, literally, the probability of the event occurring at time $t$ for a given value of $x$.

Note that, as with normal regression, it is possible to have more than one feature ($x_1$, $x_2$, etc) and thus more than one $\beta$ value.  In that case, the convention is to refer to all the features together using $X$, as in $$\lambda(t|x) = \lambda(t)\exp(\betaX) $

The word ‘Proportional’ in the model name points to one of the major limitations of Cox PH: It assumes that the effect of features on the base Hazard function will be constant (that is, proportional) for all values of $t$.  For example, in a Cox PH model, if a woman is 5 times less likely to die than a man at age 20, then a woman is also 5 times less likely to die at age 80.  In many situations, the proportionality assumption is not accurate, and other survival analysis techniques are necessary.

For a really great review of survival analysis, including some models other than Cox PH, check out this series of blog entries from [The Sampler](http://blog.applied.ai/survival-analysis-part1/).

Next, we’ll give Cox PH a try using `statsmodels`
