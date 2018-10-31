---
title: Simpson's paradox
author: Thinkful
team: grading
time: 45
uuid: 6737e511-e0a5-48ab-bb90-581556bb5b5d
---

Imagine you're analyzing gender differences in a university's admissions rate for graduate programs.  You compute the proportion of successful female applicants and compare it to the proportion of successful male applicants, and get the following numbers: 

|       | Applicants | Admitted |
|-------|------------|----------|
| Men   | 8442       | 44%      |
| Women | 4321       | 35%      |

Overall, women are less likely to be admitted to graduate programs at that university than men.  Intrigued, you dig deeper, and compute the proportion of successful applicants of each gender for each graduate program separately.  Then you get the following numbers (higher percentage bolded for each department):

| Department | Male Applicants | Male Admitted | Female Applicants | Female Admitted |
|------------|-----------------|---------------|-------------------|-----------------|
| A          | 825             | 62%           | 108               | **82%**         |
| B          | 560             | 63%           | 25                | **68%**         |
| C          | 325             | **37%**       | 593               | 34%             |
| D          | 417             | 33%           | 375               | **35%**         |
| E          | 191             | **28%**       | 393               | 24%             |
| F          | 373             | 6%            | 341               | **7%**          |


When broken down by department, women appear to have the same or slightly better chance of being admitted than men, exactly the opposite of what you observed above.  At this point, you may start checking your code for errors, but there's no need.  These data, drawn from evidence presented in a [1975 article about gender bias in Berkeley graduate admissions](http://homepage.stat.uiowa.edu/~mbognar/1030/Bickel-Berkeley.pdf), are a classic example of **Simpson's Paradox**[.](https://s-media-cache-ak0.pinimg.com/564x/69/5c/ff/695cff3fa14e2031521a121c013ed255.jpg)

Simpson's Paradox is the phenomenon when an average over a number of groups shows one trend, but an average for each individual group shows the opposite trend, or no trend.  Another name for Simpson's Paradox is the _lurking variable_ problem, where an unaccounted-for third variable changes the relationship between two other variables.

In the case of Berkeley, the third variable is the total number of men and women that applied to each program.  Looking at the numbers above, many more men than women applied to programs A and B, which had high admittance rates.  Women were more likely to apply to the programs with low admittance rates.  This means that overall, a man had a greater chance of being admitted not because he was a man, but because he was more likely to apply to a program that admitted a high percentage of its applicants. 

Another example involves [changes in the median wage](https://economix.blogs.nytimes.com/2013/05/01/can-every-group-be-worse-than-average-yes/?_r=0).  From 2000 to 2013, the median wage rose slightly.  Yet during the same period, the median wage for every educational group (High school dropouts, High school graduates, college graduates, etc) went down.  The lurking variable here is demographic changes in the United States over that period-- a greater proportion of Americans had college degrees in 2013 than in 2000.  Since people with college degrees get paid, on average, more than people with only a high school diploma, the overall median wage could rise for the population even as it dropped for each group.

The lesson of Simpson's Paradox is this: pay attention to how groups differ from one another before averaging across them.  Averaging a small group with a large one, or averaging multiple groups with very different demographics, can produce unexpected or illogical results.  

<div class="think-like-a-data-scientist">
    <p>When doing A/B testing, hopefully all your participants will have an equal chance of being assigned to see version A or version B, and both your groups will be equal in size.  By using randomization to equalize lurking variables like demographics, we can avoid Simpson's Paradox.  Because randomization is random, however, there is <em>always</em> the chance that your groups will end up with some lurking difference.</p>

    <p>Always do what you can to confirm the groups are similar before interpreting your results.  Make it a habit to look at subgroups within your A/B test to make sure the overall trend is reflected in the subgroups.  If the subgroups differ from the overall trend, your question should guide whether you report conclusions based on the overall sample, the subgroups, or both.  You don't want to advocate for condition A, even if it performs better overall, if condition B <em>actually works better within every subgroup</em>!</p>
</div>

For a deep dive into the data of Simpson's Paradox, check out [this Technical Report from UCLA](http://ftp.cs.ucla.edu/pub/stat_ser/r414.pdf).
