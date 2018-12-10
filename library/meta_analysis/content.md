---
title: Meta analysis
author: Thinkful
team: grading
time: 60
uuid: 3773f455-f62e-4762-aa79-28178b874afe
---


No matter how perfectly designed, one experiment alone is never 100% definitive.  There’s that pesky less than 5% chance of a false positive when using p < .05 as a threshold.  There’s the chance that, totally randomly, our sample is not representative of the group we want to study.  And then there’s all the uncontrollable, unmeasured (and possibly unmeasurable) factors (weather, a manufacturing error when producing an experimental medication, some participants take an unreasonable dislike to the experimenter, etc) that can throw off the results of a study.   For this reason, science emphasizes *replication*- running the same or very similar studies more than once, ideally in different laboratories, to see if they get the same finding.  The more times a study replicates, the more likely its findings are to be true.

## Two Truths and a Lie: Aggregating Study Results
Alright, imagine we have three studies all comparing the effects of 20 mg of drug X to a placebo (a sugar pill designed to make people think they are getting a drug), with the intention of treating underactive thyroid (hypothyroidism).  The results, measured via levels of thyroid-stimulating hormone (TSH)  in the blood, are:

| Study | Drug X | Placebo | p1  |
|-------|--------|---------|-----|
| 1     | .08    | .51     | .04 |
| 2     | .15    | .63     | .01 |
| 3     | .39    | .45     | .14 |

Since two studies show a significant effect for Drug X, and one study shows no effect, we could go with majority rule and conclude that Drug X works.  Yay!  Pharmaceutical Company Druginex, makers of Drug X, celebrate. 
But wait.  We know that not all studies are created equal:
* Representative samples are better than studies with non-representative samples.
+ Imagine that study 2 has only men in it, yet Drug X is marketed to both men and women.  Problem! 
* Studies may focus on different populations:
	* If Study 1 is on adults over 65, and Studies 2 and 3 are on adults in their 30s, they can’t be directly compared.
* Studies with larger samples are better than studies with smaller samples.
	* If the N of Study 3 is four times larger than the Ns of Studies 1 and 2 combined, Druginex might need to cancel their party. 
* Studies may have important variation in methods.
	* **Timeline variation**: Perhaps the timeline for Study 3 is only 1 hour between taking the drug and measuring the thyroid hormones, while the timelines for Studies 1 and 2 are 1 day.
	* **Dosage variation**: Study 2 gives participants 20 mg of Drug X, while Study 1 gives them 10 mg and Study 3 gives them 5 mg.


## Methods of meta-analysis
We call meta-analysis an approach, rather than a model or an algorithm, because it isn’t a statistical technique- it is a way of combining studies that uses various statistical techniques depending on the demands of the data and the question at hand. 

### Finding studies
Just like a normal statistical analysis is only as good as the data, a meta-analysis is only as good as the studies it contains.  A major component of meta-analyses is establishing a transparent and unbiased method of finding all the relevant studies on a topic.  Modern scientific databases such as the [Open Science Framework](https://osf.io/preprints) and [PubMed](https://www.ncbi.nlm.nih.gov/pubmed/) make it almost too easy to pull all the articles on a particular topic.  Often the majority of search results won’t be relevant to the meta-analysis, and a logical strategy for identifying relevant articles and filtering out irrelevant ones will be necessary. 

### Sample weights
For a simple situation where the studies are matched in all ways except sample size, a meta-analysis could involve simply *weighting* the scores by the sample size.  Using weights causes a study with a larger sample size to have more influence on the overall mean (or other statistic) than smaller studies.  This can be as simple as multiplying each study’s scores by the sample size, adding them up, and then dividing by the total sample size.

### Effect sizes
In our opening sample, all three studies used the same outcome measure- thyroid hormone levels in blood.  This sort of homogeneity is rarely the case in real life.  One study might use thyroid in blood, another thyroid in spit, and a third infer thyroid levels by measuring body temperature (low thyroid  means low body temp).  In this case, basic averaging makes no sense.  Instead, many meta-analyses convert study scores to **effect sizes**.  [There are many effect sizes](http://www.theanalysisfactor.com/effect-size/).  One of the simplest and most common is called *Cohen’s d* and is simply the difference in scores between two groups divided by the standard deviation:
$$ d = \frac{Mean1-Mean2}SD$

In words, Cohen’s d scales the size of the difference between the two groups by the amount of noise/variability in the data.  No matter what measurements you use (blood hormones, spit, etc), it is easy to compare group differences when they are all converted to fractions of a standard deviation.  Originally, Cohen provided some interpretive guidelines for *d*: .2 was a small effect, .5 is medium, and .8 is large.  In other words, a difference of two-tenths of a standard deviation between two group is a small effect.

If the formula for Cohen’s *d* seems familiar, you may be thinking of the formula for a *t-test*, the statistical test to determine if two group means are statistically significantly different from one another.  The formulae are very similar,  but the t-test divides by the standard *error* ($\frac{SD]{N-1}$ rather than the standard *deviation* ($SD$).  This means that the p-value, which is based on the sample size (N) and the t-value, is not the same as the effect size: A finding can have a very low p-value but a small effect size (this often occurs with large sample sizes), or a large effect size but a non-significant p-value (which often occurs with small sample sizes).

### Publication Bias
While in principle a null finding (a finding of no difference between groups, for example) is just as meaningful to science as finding an effect.  In practice, journals tend to publish positive findings at a much higher rate.  There are a lot of reasons for this, from courting publicity (‘Drug Y Cures Cancer!’ is a much better headline than ‘Drug Y Does Nothing’) to the mistaken belief that positive findings are more ‘reliable’ than null findings.  It is true that there’s no way to conclusively *prove* that an effect doesn’t exist (there’s always something an experimenter could have missed or messed up), but a well-designed study should be trustworthy (and publication-worthy) no matter what it finds.

As a result, the body of published studies on a topic rarely, if ever, represents all the studies that have been done.  Sometimes null findings get rejected by journals, but often scientists don’t even try to submit them- the so-called ‘file drawer’ problem.   Meta-analyses try to correct for this problem in many ways.  First, the researchers may send out an email to people known to do these kinds of studies, asking for any ‘file-drawered’ results.  Second, there are statistical methods to try and detect, then correct for, publication bias.

The most common method for detecting publication bias is to create a funnel plot, where each study represents a datapoint.  The x-axis is the effect size, and the y-axis is the inverse of the standard deviation (1/SD).  If the funnel plot is approximately vertically symmetrical, then publication bias may not be a concern.  If the plot is asymmetrical, with what looks like many datapoints ‘missing’ on one side, this is an indication that studies with smaller or potentially nonsignificant effects are not being published.  Correcting for this bias once it is detected is complex.  The most straightforward method is called [trim-and-fill](https://www.researchgate.net/profile/Sue_Duval/publication/254287922_A_Nonparametric_Trim_and_Fill_Method_of_Accounting_for_Publication_Bias_in_Meta-Analysis/links/55ad72bd08aed9b7dcdae32e/A-Nonparametric-Trim-and-Fill-Method-of-Accounting-for-Publication-Bias-in-Meta-Analysis.pdf).  

In practical terms, trim and fill takes an asymmetrical funnel plot and makes it symmetrical by removing (‘trimming’) the points that have no counterpart on the opposite side.  Then they estimate the mean effect size using only the ‘symmetrical’ points, and use this new center and the ‘trimmed’ values to estimate the values that, by inference, would need to be present to create a symmetrical plot from the original full set of effect size estimates (including the ‘trimmed’ ones).

### Modeling

Calculating effect sizes and correcting for bias can be thought of as the ‘data cleaning’ step of meta-analysis.  The next step is to analyze the data.  Happily, once the data is cleaned it can be treated like any other data.  One popular technique is to run a regression predicting effect sizes using study characteristics such as gender of participants, location, drug dosage, etc.  This approach requires a large number of studies to really work, but it can yield really great insights into factors that can moderate (change) the effects of a drug.  There is even such as thing as weighted regression, so that sample sizes can be incorporated into the calculation of regression estimates.

## Summary

Meta-analyses are incredibly valuable, especially in areas such as Biostatistics where research results are often translated directly into medical treatments.  They help to determine not only whether a drug or therapy is better than an alternative, but also how large the effect is, and the conditions under which it works best.  

