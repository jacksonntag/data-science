---
title: Challenge
author: Thinkful
team: grading
time: 480
---

In this module, we learned how to approach and solve regression problems using linear regression models. Throughout the module, you worked on a house price dataset from Kaggle. In this challenge, you will keep working on this dataset.

## The scenario

The housing market is one of the most crucial parts of the economy for every country. Purchasing a home is one of the primary ways to build wealth and savings for people. In this respect, predicting prices in the housing market is a very central topic in economic and financial circles.

The house price dataset from Kaggle includes several features of the houses along with their sale prices at the time they are sold. So far, in this module, you built and implemented some models using this dataset.

In this challenge, you are required to improve your model with respect to its prediction performance.

To complete this challenge, submit a Jupyter notebook containing your solutions to the following tasks.

## Steps

1. Load the houseprices data from Thinkful's database.
1. Do data cleaning, exploratory data analysis, and feature engineering. You can use your previous work in this module. But make sure that your work is satisfactory.
1. Now, split your data into train and test sets where 20% of the data resides in the test set.
1. Build several linear regression models including Lasso, Ridge, or ElasticNet and train them in the training set. Use **k-fold cross-validation** to select the best hyperparameters if your models include one!
1. Evaluate your best model on the test set.
1. So far, you have only used the features in the dataset. However, house prices can be affected by many factors like economic activity and the interest rates at the time they are sold. So, try to find some useful factors that are not included in the dataset. Integrate these factors into to your model and assess the prediction performance of your model. Discuss the implications of adding these external variables into your model.

