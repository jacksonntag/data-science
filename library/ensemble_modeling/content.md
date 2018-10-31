---
title: Ensemble modeling
author: Thinkful
team: grading
time: 5
uuid: 71dea2b6-f889-4d1f-a506-8abcf492d94c
---

Introducing Random Forests leads us to another, much larger, topic: **Ensemble models**. Ensemble models are essentially models _made up of other models_. These component models are often models that are simpler than would be necessary to accurately predict the desired outcome on their own. In the case of Random Forest, those sub models are Decision Trees. Random Forest generates many Decision Trees and combines them to generate a single prediction via a voting process.


## Methods of Ensemble Modeling

There are many kinds of ensemble models. In fact, there are infinite kinds of ensemble models because you can combine most kinds of models together and create a new kind of ensemble model by mixing and re-mixing different component models. However, most ensemble models fall into three main categories.

**Bagging** is one such ensemble technique. In bagging you take subsets of the data and train a model on each subset. Then the subsets are allowed to _simultaneously_ vote on the outcome, either taking a majority or a mean. You just saw this in action with Random Forests, the most popular bagging technique.

Another ensemble technique is called **boosting**. Rather than build multiple models simultaneously like bagging, boosting uses the output of one model as an input into the next in a form of _serial_ processing. These models then get daisy-chained together sequentially until some stopping condition is met. We’ll cover boosting methods later.

Lastly, **stacking** is a two phase process. In the first phase multiple models are trained in parallel. Then in the second phase those models are used as inputs into a final model to give your prediction. This approach combines the parallel approach embodied by bagging with the serial approach of boosting to create a hybrid of the two.

You can create your own ensemble methods by manually combining models, but there are already several widely used forms of ensemble learning in use. We'll cover these later in the course. Random Forest is really just the tip of the iceberg.

<div class="think-like-a-data-scientist">

<p>There are advantages and disadvantages to ensemble models. Most notable is of course their performance. Ensemble models are often some of the most accurate techniques to apply to a problem. They also tend to have low variance because they're built from multiple internal models.</p>


<p>However there are also downsides. Most notably, some ensemble techniques, particularly boosting, are prone to overfitting. You also lose a lot of the transparency that individual models offer. You saw this clearly in the Random Forest example, where the easy explanations offered by decision trees are abstracted away by the forest.</p>
</div>

