---
title: A/B testing
author: Thinkful
team: grading
type: graded
time: 45
uuid: 27916d10-4041-4b07-9435-35e1da6d5d7e
---

In this checkpoint, we explore A/B testing, which is a common approach to identify which of two versions of some entity performs better with regard to a desired outcome.

## The ABCs of A/B testing

[There are lots of different possible experimental designs](https://cirt.gcu.edu/research/developmentresources/research_ready/experimental/design_types), but **A/B testing** is probably the most common in business and the one you are most likely to encounter.  A/B testing is a technique used to identify whether one version of an object of interest (product, marketing campaign, email text) is better at producing a desired outcome than another.

The components of an A/B test are:

 * **Two versions** of something whose effects will be compared. Typically one version is a "control version," often already in use (or "no intervention"), and one is a "test version," which has some changes from the control. That change is often called the _treatment_. If starting from scratch, however, you may have two different test versions to compare to each other.
 * A **sample**, divided into two groups. Each sample should be selected so that it is similar to the population you want to understand. The groups should be similar to one another so that any differences between them can be attributed to seeing version A or version B and not something else. You also want the split of between A and B to be as random as possible.
 * A **hypothesis**. Your hypothesis is what you expect to happen. For example, "I expect the HTML email will achieve a higher open and conversion rate than the plain text email."
 * **Outcome(s)** of interest. What you expect will change as a result of using version A or version B, and how you will measure that change. This means you have to decide on a _key metric_, which should capture the effect of your change and reflect the motivations for the test in the first place.
 * **Other measured variables**. This includes information about the two groups that can be used to ensure they are similar, as well as secondary outcomes that are less important than the primary outcomes of interest but which might _also_ change in response to using version A or version B.


## Getting a Good Sample

One of the key elements of an A/B test, as we said above, is the sample. Particularly important when it comes to actually designing your own experiment is making sure that the two groups, the A and B, are as comparable as possible. The only difference should be the treatment they receive.

Now, if you have a constantly occurring easily randomizeable test, where the thing you're interested in measuring is happening all the time in easily separable occurrences, this is pretty easy. Something like marketing emails are usually like this. Thousands of emails are being sent out all the time and you can easily randomize between A and B.

However, plenty of things can make this more complex. The most common challenge is a test that either has to be "all on" or "all off". This could be something like whether playing music in a shop makes people stay longer. You really can't have some people in the shop hearing the music and others not. 

In that case getting to randomization becomes an art form. You want to think about things like seasonality – making sure there is no difference in your two groups because of day of week or time of year. Perhaps behavior is just different on weekends, at nights, or in the summer.


## Keys to Key Metrics

The other major sticking point is picking what you want to measure, your outcome. You can, and should, monitor many metrics during most tests, but you typically want to have one _key_ metric that will be your determining factor for whether a test is successful or not.

There are several things that make a good key metric. Firstly you want it to be as closely related to your business goal as possible. Measuring clicks is good, but if it makes sense you'd rather measure sales or purchases. This helps prevent getting a result that just affects an intermediate step without improving the actual goal. Just because people engage doesn't mean they'll follow through.

You also want your key metric to be reliably measurable. It seems obvious, but many experiments are ruined by measurement error. Ideally this means something that is passively recorded, rather than requiring an additional engagement from subjects or users. You also generally want to avoid self reported data, because that invites its own host of potential biases.

As much as possible, you also want to capture the complete effect of your change. Sometimes this may mean time becomes important. Maybe an email campaign doesn't lead to an immediate increase in sign ups, but customers convert later. Trying to include a window of impact that's both reasonable and still consistent across all observations is a valuable characteristic for your metric.


## This is a test

Let's go through an example. If we were trying to improve the clickthrough rate of an email campaign, we might test two newsletters, one with _black italic text_ and one with <strong style="color:#6AA84F">green bold text</strong> and an exclamation point ("_Sale Today_" vs "<strong style="color:#6AA84F">Sale Today!</strong>"; our two versions).  

We would then randomly send one of the two versions of the email to a subset of subscribers to our newsletter (all subscribers who get an email represent our sample, and all subscribers that get the same version of an email represent one of our two experimental groups), and track the number of clicks each version generated (our outcome of interest).  

We expect that the <strong style="color:#6AA84F">green bold text</strong> will result in more clicks (our hypothesis).  We may also want to look at the gender and age of our sample, if we have that information, to make sure the groups are similar. We can also look at whether the two different newsletters affect how quickly people open the email after receiving it (a secondary outcome) as well as the click rate.

If the two groups appeared similar in age, gender, and anything else we measured, but click rates were higher for the <strong style="color:#6AA84F">green bold text</strong> version of the newsletter, we would conclude that changing the text to be green and bold caused more clickthroughs. As a result, we would advocate for including <strong style="color:#6AA84F">green bold text</strong> in all future newsletters.


## Assignments

For each of the following questions, outline how you could use an A/B test to find an answer. Be sure to identify all five key components of an A/B test we outlined above.

 * Does a new supplement help people sleep better?
 * Will new uniforms help a gym's business?
 * Will a new homepage improve my online exotic pet rental business?
 * If I put 'please read' in the email subject will more people read my emails?