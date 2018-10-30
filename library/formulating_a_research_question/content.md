---
title: Formulating a research question
author: Thinkful
team: grading
time: 120
uuid: 802728a5-0cc1-4a7c-9796-35491aa90d9b
---

In this checkpoint, we'll discuss how to go about formulating a good research question for data modeling. 

One way to think of a statistical model is as the _mathematical expression of a research question_. In supervised learning, we begin with an outcome of interest, a particular variable that we want to understand, explain, and/or predict.  ur research question, in relation to that outcome, may be as broad as "How do we best predict the outcome of interest given the data?" or as narrow as "What is the most accurate estimate of the outcome of interest for N groups under X conditions?" The research question will guide your model-building and data exploration by spotlighting variables and inter-variable relationships of particular interest.

Different types of research questions also call for different types of models. Research questions about odds or likelihood, such as "will it rain today in Omaha?", use models specifically designed to deal with binary outcomes (either it rains or it doesn't).  Research questions about quantity, such as "how much will it rain?", use models that deal with continuous outcomes.

As a data scientist, you may be provided with a research question to answer, and your job will be to translate it into a statistical model. But that isn't always the case. Defining your own research question is a more involved process, and there are many questions you'll want to ask yourself as you go about that process, such as:

* _What is already known about this topic?_  Unless your goal is simply to learn a new statistical method and the research question itself is irrelevant, there's no point in reinventing the wheel.
* _What sort of data, or ways to collect data, are available to me on this topic?_  A research question without relevant data is simply speculation.  
* _What skills do I have?_  A research question should be addressable using the statistical and programming skills you have now, or can feasibly learn in the time budget you have.
* _Can this question be answered using quantities or probabilities?_  Since the plan is to address this research question using a mathematical model, it must be amenable to a numeric solution.
* _Can this research question be asked in one sentence?_  If you need more than one sentence to explain what you want to know, your question is probably too broad or too vague to be useful and needs refining.

While a well-defined research question will exclude some modeling options (models for categorical vs continuous outcomes, for example), many degrees of freedom remain for the data scientist when defining a model. [Kaggle Competitions](https://www.kaggle.com/competitions) offer some fantastic examples of the many models that can be used to answer the same research question.

## Assignment

Categorize each of the following research questions as "good" or "bad", and provide alternative formulations for the bad ones.  Save your responses in a document of some kind, submit a link below, and discuss your reasoning with your mentor.
 1. What is the 1994 rate of juvenile delinquency in the U.S.?
 2. What can we do to reduce juvenile delinquency in the U.S.?
 3. Does education play a role in reducing juvenile delinquents' return to crime?
 4. How many customers does AT&T currently serve in Washington, DC?
 5. What factors lead consumers to choose AT&T over other service providers?
 6. How can AT&T attract more customers?
 7. Why did the Challenger Shuttle explode?
 8. Which genes are associated with increased risk of breast cancer?
 9. Is it better to read to children at night or in the morning?
 10.  How does Google’s search algorithm work?