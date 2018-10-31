---
title: Regression vs. classificaiton
author: Thinkful
team: grading
time: 60
uuid: 154a959a-c084-49d4-9a16-fdfd71448e0e
---

When building a model, the first question to ask is: "What kind of model do I need to build?" There are many many possible answers to that question, so it's worth working from the top down. We've already said that this Unit will be about supervised learning and covered a little bit about what that means. Within supervised learning there are two main groups: **classification** and **regression**. This checkpoint will focus on the distinction between those two categories and how you choose which kind of model you want to build.


## Classification

Let's discuss classification models first. When building a supervised model, there is always some kind of outcome we're interested in. What kind of variable that is informs what kind model we are going to build.

For a classification model, that variable will be **categorical**. This means that the variable only takes discrete values from within a specified set. Simple versions of that set could look something like {yes, no} or {heads, tails}. The outcomes could also contain more than two values such as {high, medium, low} or {buy, rent, no purchase}. Almost anything that can be discretely counted and labeled can be considered a categorical variable. In the earlier assignment on feature engineering we discussed the three kinds of categorical variables: ordinal, interval, and ratio variables.

So, given this, the outcome of a classifier is typically one of two things. It will either assign a category to a given test observation or it will assign a probability of each category. This means say if the potential outcomes were {yes, no}, for a given test row the output of a classifier would either be {yes} or {no} or some probability measure for each such as {.2, .8}.

It is important to note that with a classifier, the only outcomes that will be seen as possible _have_ to be in the training set. So if your test set has a value for the outcome variable that was not in the training set it will not be able to predict it correctly. One example could be if you were trying to predict the show that someone would watch on a movie website and a new movie was released. If that movie isn't in the training set you can't predict if people will watch it.


## Regression

In contrast to classification, regression models have a continuous outcome variable. As such regressions can output either on a bounded or unbounded number line. That also implies a relationship between the variables. This simply means something like 3 is greater than 2 is greater than 1, and the intermediate values imply just that, they are between each other. 

Example variables that would work for regression would be something like _amount spent_ which could range from 0 to some potentially very large observable max, or _temperature_ which ranges from absolute zero to again observably high (though any model would likely concentrate output in a more specific region). Many regression techniques can give predictions even beyond observed maxima and minima, while others are more bounded.

<div class="think-like-a-data-scientist">

<p>So what if the outcome you're interested in is the number of cars owned {0, 1, 2, 3, 4, 5} and you've never seen someone with more than 5. Should you use regression or classification?</p>

<p>The fact is you could use either. If you use classification then for each observation you're only going to be able to evaluate the likelihood of each given value. Each outcome level will be treated discretely and the relationship between them is not predefined. But if you use regression you're going to find their most likely place along a continuous line, without necessarily even having bounds at zero or 5. Each approach has its advantages, and which one you'll want to use will depend on how you want to use the output. Keep in mind a classifier generally does not average these outcomes for you, so if you're just getting a single output it will give you the most likely outcome, not the average.</p>
</div>

## Assignment

For each of the following situations, decide if you would model using a regression or classification model. Discuss your reasoning with your mentor next time you meet.

 1. The amount a person will spend on a given site in the next 24 months.
 2. What color car someone is going to buy.
 3. How many children a family will have.
 4. If someone will sign up for a service.
 5. The number of times someone will get sick in a year.
 6. The probability someone will get sick in the next month.
 7. Which medicine will work best for a given patient.

Submit a link to your work below.
