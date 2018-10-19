---
title: Basics of probability
author: Thinkful
team: grading
type: graded
time: 240
uuid: 78ce2724-6c33-4161-b028-aec860d09cb0
---

>It is remarkable that a science which began with the consideration of games of
chance should have become the most important object of human knowledge. –Pierre Simon Laplace, _Théorie Analytique des Probabilités, 1812_

One of the reasons data science is in such high demand is because organizations want to predict the future. With the right dataset, a data scientist can create models that give information about how likely certain outcomes will be. Those models help organizations steer toward desired outcomes, turn away from negative ones, and create successful businesses.

To accurately predict, you need to be able to apply basic principles from probability, and in this checkpoint, we'll cover those. We'll review the following topics:

* Frequentist vs. Bayesian approaches
* randomness
* sampling
* selection bias
* independent vs. dependent events
* Bayes' rule


This checkpoint ends with a set of drills where you'll apply what you've learned.

## Perspectives on probability: frequentist vs. Bayesian

Probability is a way of quantifying the likelihood of a future outcome. People use probabilities to make decisions all the time. Knowing the probability of rain tomorrow helps to decide whether to put the rainboots and umbrella in the car tonight. 

There are two broad schools of thought about probability in statistics. The *frequentist* school of thought defines probability as describing how often a particular outcome would occur in an experiment if that experiment were repeated over and over. For example, each time a coin is flipped, the outcome is either 1 (heads) or 0 (tails). Each coin flip is an "experiment" with an outcome. Over many coin flips, the coin will come up heads about 50% of the time. For a frequentist, saying an outcome has a 50% probability is equivalent to saying that if the experiment were repeated many times, that outcome would occur 50% of the time. 

The *Bayesian* school of thought defines probability as describing how likely an observer expects a particular outcome to be in the future, based on previous experience and expert knowledge. Each time the experiment is run, the probability is updated if the new data changes the belief about the likelihood of the outcome. The probability based on previous experiences is called the "prior probability," or the "prior," while the updated probability based on the newest experiment is called the "posterior probability."

Both Bayesian and frequentist approaches to probability are used to model data, depending on the question being asked. Disagreements between the two camps can [get](https://xkcd.com/1132/) [heated](http://www.smbc-comics.com/index.php?id=4127), but there's no need to take sides: Most of the time, the Bayesian and frequentist approaches arrive at the same answer. A good rule of thumb is that frequentists are trying to calculate the likelihood of getting the data you have in the context of a fixed, if unknown, "true" population value. Bayesians are trying to calculate the most likely population value, given the data you have. As the data changes, Bayesians beliefs about the population value change as well.

For a more in-depth discussion with complex examples of how frequentist and Bayesian approaches can be used to answer a question, including code in Python, see this [series of articles by Jake Vanderplas](http://jakevdp.github.io/blog/2014/03/11/frequentism-and-bayesianism-a-practical-intro/)

## Randomness, sampling, and selection bias

The concept of probability is fundamental to data science.  A lot of the value a data scientist brings comes from the ability to *quantify uncertainty* – to go from a vague and woolly "maybe it will rain" to a clear and precise "65% chance of rain with a margin of error of 3%."  Quantified uncertainty not only defines what is known, but how confident we can be about that knowledge.  

Probability is also the fundamental basis of another critical element of the data scientist's toolkit: *Randomness*.  Randomness can be defined as a situation where all possible outcomes are equally likely.  The flip of a balanced coin is random: 50% likely to be heads, 50% likely to be tails.  The roll of a six-sided dice is also random, with a 1 in 6 chance of getting each number between 1 and 6.  

It is rarely possible to gather data from all elements of a population of interest (can't get questionnaires to all potential customers around the world, can't get information about purchasing decisions that haven't happened yet).  Instead, data scientists leverage the concept of randomness to gather a representative sample from the population.  Using randomness, each element of a population has an equal chance of being chosen for the sample.

In an ideal world, <strong>random sampling</strong> creates a smaller group (a sample) that is sufficiently similar to the population that anything we learn about the sample also applies to the population.  Larger samples are more likely to resemble the population, because they are less swayed by the occasional extreme value.  On the other hand, smaller samples may be cheaper and faster to collect.  Deciding how large a sample to collect depends in part on how variable we think the population is: the more variability in the population, the larger sample we need to get to be confident that our sample is a good stand-in for the population.  However, it is important to keep in mind that the sample is *random*: It may, through sheer dumb luck, sample enough unusual individuals to be unrepresentative.

In practice, random sampling depends on perfect access to the population, which is very rarely possible.  When studying customers, for example, not all customers may be interested in or willing to participate in data collection.  The sample, in that case, differs from the population of all customers: The customers in the sample are all people who are willing to be studied.  Systematic differences between the sample and the population are known as *selection bias*.  If the sampled individuals differ from the others in important ways, such as spending rates or purchasing behavior, then knowledge gained from their data might not apply to all customers.

### Selection bias: a practical example

An example from US history illustrates the pitfalls of generalizing from a biased sample.  The 1936 US Presidential election pitted Alfred Landon against Franklin D. Roosevelt.  The largest pre-election poll of the time, conducted by the respected magazine _Literary Digest_, projected that Landon would beat Roosevelt by 14%.  This projection was based on ballots sent to 10 million US citizens, nearly a quarter of all eligible voters at the time.  Yet the _Literary Digest_ turned out to be impressively wrong, with Roosevelt beating Landon by 24%.  The poll was off by an astounding 38%.  How did this happen?

The _Literary Digest_'s sampling efforts, though broad, were flawed: they sampled people by drawing from the telephone directory.  In the middle of the Great Depression, phones were luxuries many could not afford.  The Digest's methods led to a sample that was considerably older and richer than the general population… with predictable results for their election forecast.  When it comes to sampling, it is better to have a small but representative sample than a large and biased one.

For more details on the Literary Digest poll, see [this case study](https://www.math.upenn.edu/~deturck/m170/wk4/lecture/case1.html).


## Dependent vs. independent events

When talking about probabilities of events, whether Bayesian or frequentist, one important consideration is whether the events are independent or dependent of one another.  An event is independent of other events in the sample space if the outcome of that event is not affected by the outcome of other events in the sample space. For example, imagine a bag of 10 marbles, containing 5 blue marbles and 5 red marbles. Without looking, you reach into the bag and draw out a red marble.  Then you put the marble back in the bag, and draw a blue marble. The probability of drawing a red marble first is 5/10, or 50%. The probability that the second marble will be blue is also 5/10, or 50%. Because you put the first marble back, the probability of drawing the second marble is independent of the first. Neither event affects the other.

The probability of drawing and replacing a red marble:

```
P(red) = 1/2
```

`P` in the formula above means "probability".

The probability of drawing and replacing a blue marble after drawing and replacing the red marble):

```
P(red) = P(blue) = 1/2
```

The probability of two or more independent events can be calculated by multiplying the probabilities of each individual event. The probability of drawing a red marble and then a blue marble:

```
P(red ∩ blue) = P(red) * P(blue) = (1/2) * (1/2) = 1/4
```

When the probability of event B changes based on the outcome of event A, the probability of event B is said to be dependent on, or *conditional* on, event A.  Returning to the bag of marbles, again you reach into the bag and take out a red marble.  Again, the probability that the first marble will be red is 5/10 or 50%.  

```
P(red) = 1/2
```

Next, without replacing the red marble, you draw a blue marble.  Now, the probability of drawing a blue marble depends on the color of the first marble drawn.  We use `|` to denote a condition on the probability we're talking about. This is where the information we already have can be disclosed.

If the first marble was blue, then the probability of drawing a red marble the second time is 5/9 (because one blue marble is missing from the bag).  

```
P(red | blue) = 5/9
```

You can read the `|` symbol as "given", so `P(red | blue)` would read "the probability of red given blue".

If the first marble was blue, then the probability of drawing a blue marble the second time is 4/9 (because one blue marble is missing from the bag).  

```
P(blue | blue) = 4/9
```

The probability of drawing a blue marble the second time is conditional on the outcome of the first draw.

The probability of two conditional events can be calculated by multiplying the probability of event A by the probability of event B conditioned on A.

```
P(A ∩ B) = P(A) * P(B | A)
```

The probability of drawing two blue marbles in a row without replacement:

```
P(blue) * P(blue | blue) = (1/2) * (4/9) = 2/9
```

The probability of drawing a red marble and then a blue marble without replacement:

```
P(red) * P(blue | red) = (1/2) * (5/9) = 5/18
```

In data, conditional variables (conditional and dependent are synonymous, however, because a 'dependent variable' has a specific meaning in experimental design, we will use *conditional* when referring to variables) in a dataset contribute less information than independent variables, because some information is duplicated among conditional variables. For example, a survey may ask four questions: 1) a customer's age, 2) their income, 3) whether they bought any widgets that month, and 4) how much money they spent on widgets that month.

The age and income variables are independent in the sample space: While knowing someone's age may give some hints about their income, there is enough variability in incomes between people of the same age that every datapoint is giving new information. Similarly, while the income variable is probably related to how much money people have available to spend on widgets, people with the same income may buy different amounts of widgets (or no widgets at all), so each datapoint provides new information for both variables.  

Questions three and four, on the other hand, are conditional.  If someone says that they didn't buy any widgets in the last month, we <em>already know</em> they spent $0 on widgets.  Conversely, if someone says they spent $0 on widgets last month, we <em>already know</em> they didn't buy any widgets.  The two variables aren't perfect duplicates, since knowing someone did buy one or more widgets isn't the same as knowing how much money they spent, but for at least some cases, knowing the answer to question 3 means we can be 100% certain that we know the answer to question 4 (and vice versa).

## Bayes' rule and conditional probability

On a random day you see a pop up clinic for an instant test for a new disease you’ve heard of: Weapon X. It’s an incredibly rare disease with almost no symptoms for months and then you suddenly die. It’s affecting about one in a million people, from what you’ve heard. This test says it’s 99.99% accurate in both directions (false positives and false negatives), so you decide it’s worth taking the test.

It comes back positive.

Should you panic?

Bayes' Rule explains that, in actuality, you’re probably just fine.

In this scenario we’re not focused on the probability of an independent event. It’s not the probability that you are infected with Weapon X. It’s the probability that you’re infected _given the condition_ that you get a positive test.

That positive test provides additional information about what’s going on, and we can use that information to improve our probability estimate.

For this example, let’s say we have a million people. Chances are one of them is infected, since the disease affects one in a million, and that person will likely get a positive test result. However, if we tested every one of those other 999,999 people, we’d expect about 100 people to get positive results. 

Once you see that positive test, what do we know about your likelihood of being infected? Since we know you have a positive test, we can consider only the people in that group who have seen a positive test result. In that group are 101 people, only 1 of whom actually has the infection. This works out to roughly 1% chance that you’re infected.

Now, these counts are a bit of a simplification, using expected counts rather than probabilities. Bayes' rule gives you this relationship in terms of probabilities.

### Bayes' Rule

Bayes' Rule can be put in its simplest and most abstract terms as follows:

```
P(A | B) = P(B | A) * P(A) / P(B)

OR

P(A | B) = P(B | A) * P(A) / [P(A)*P(B|A) + P(A~)*P(B|A~)]
```

In English, this formula says the probability of A given B equals the probability of B given A, times the probability of A, divided by the probability of B. We expand the probability of B in the second formula where A~ is the inverse of A, so in our case not being infected. The numerator is our scenario of interest, while the denominator represents the realm of scenarios that could give our condition.

We can put that in terms of our example pretty simply.

```
P(Infected| Positive Test) = P(Positive Test| Infected) * P(Infected) / P(Positive Test)

= .9999 * .000001/(.000001*.9999 + .999999*.0001) = .0099 or .99%
```

So that says it’s less than 1% that you’re actually infected, which is still reasonably unlikely.

This may seem like a detached example, but this really happens. In general, people can be very bad at this kind of probabilistic reasoning. In one example in New York and San Francisco, [clinics stopped using a rapid HIV test because it was scaring healthy people](http://www.nytimes.com/2005/12/10/health/false-positives-from-hiv-test.html?_r=0). It’s why a lot of these tests get run multiple times before their results are given. The first response to a test suggesting an individual has a rare disease is usually to run it again.

## Assignments

Now it’s time to compute some probabilities. Keep track of your work in a Google document or markdown file that you can share with your mentor.


### Drill set 1

 1. Calculate the probability of flipping a balanced coin four times and getting each pattern: `HTTH`, `HHHH` and `TTHH`.
 2. If a list of people has 24 women and 21 men, then the probability of choosing a man from the list is 21/45.  What is the probability of not choosing a man?
 3. The probability that Bernice will travel by plane sometime in the next year is 10%.  The probability of a plane crash at any time is .005%.  What is the probability that Bernice will be in a plane crash sometime in the next year?
 4. A data scientist wants to study the behavior of users on the company website.  Each time a user clicks on a link on the website, there is a 5% chance that the user will be asked to complete a short survey about their behavior on the website.  The data scientist uses the survey data to conclude that, on average, users spend 15 minutes surfing the company website before moving on to other things.  What is wrong with this conclusion?

When you're done, the solution for this drillset can be found [here](https://github.com/Thinkful-Ed/data-201-resources/blob/master/solutions/Prep%20course/3.2.4.md).

## Drill set 2

Now it's time to use Bayes' rule to compute some conditional probabilities. First look over the numbers and estimate each of the four probabilities, using your intuition. Then, calculate the probabilities using Bayes' rule. Keep track of your work in a Google document or markdown file that you can share with your mentor.

A diagnostic test has a 98% probability of giving a positive result when applied to a person suffering from Thripshaw's Disease, and 10% probability of giving a (false) positive when applied to a non-sufferer. It is estimated that 0.5 % of the population are sufferers. Suppose that the test is now administered to a person whose disease status is unknown. Calculate the probability that the test will: 

 1. Be positive
 2. Correctly diagnose a sufferer of Thripshaw's
 3. Correctly identify a non-sufferer of Thripshaw's
 4. Misclassify the person

Were your intuitions on the mark, or way off? If your statistical intuition is leading you astray, you aren't alone. According to Nobel-prize winning Daniel Kahneman, [humans simply are *not* good intuitive statisticians](http://www.burns-stat.com/review-thinking-fast-slow-daniel-kahneman/). That fact has two strong implications for you as you prepare for a career in data science:

 1. Just because your statistical intuition is wrong does *not* mean you're a bad statistician. We're all in this boat. Don't give up on yourself. And,
 2. Just because you easily intuit the answer to a statistical question does *not* mean you're right. Don't trust your intuition. Check your work.

Discuss your answer to each of these questions with your mentor.  If you want more Bayes practice, try [these exercises](http://stony.me/statistics-for-beginners-bayes-rule-4/).

After giving it a try yourself, you can find a solution [here](https://github.com/Thinkful-Ed/data-201-resources/blob/master/solutions/Prep%20course/3.2.6.md).

