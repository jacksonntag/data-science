---
title: SQL self-sufficiency exam
author: Thinkful
team: grading
time: 120
uuid: 8db7ccf0-f049-47c4-bc7c-d0a13aa7097b
---

In this checkpoint, you'll complete the SQL self-sufficiency exam. The point of this exam is for you to demonstrate your mastery of commonly-used SQL skills. This exam is designed to have you work through generating some realistic SQL queries you might need to do in a professional setting.

First, we'll describe the business scenario that frames this exam. Then, we'll provide the credentials to connect to the database. Finally, we'll provide a list of prompts that require you to write SQL queries. 

To complete this exam, you should submit a single text file that contains the queries you generated for each prompt. You can indicate which question the query is for by using a code comment like this:

```sql
-- 1

SELECT....

-- 2

SELECT....
```

Your answers to each prompt will be evaluated on two criteria. First, the grader will look to see that you have created the *correct* query. For each of the prompts below, there is a single, correct answer. Second, the grader will look at how you've styled your queries. They'll look to see that you're following the recommended style guidelines for this program (especially around capitalizing SQL keywords and using lowercase for table and field names, as well as using multiple lines to make your queries more readable).


## The scenario

You're working with your state's Department of Education and in the initial stages of a project, doing some basic data exploration. You are given a database containing 2 tables: *naep* and *finance*. NAEP is the National Assessment of Educational Progress for states. The *naep* table contains each state’s average NAEP score in math and reading for students in grades 4 and 8 for various years between 1992 and 2017. The finance table contains each state’s total K-12 education revenue and expenditures for years 1992–2016.

You are tasked with assessing the quality of and finding useful ways to analyze this data.


## Connect to the database

To connect, use the following credentials:

**Host**: 142.93.121.174

**Username:** dsbc_student

**Password**: 7\*.8G9QH21

**Port:** 5432


For this exam, you'll need to use the *department_of_education* database.


## Query prompts

Below you'll find 9 numbered prompts that will require you to write SQL queries. These prompts are split up into two distinct sections focusing on data exploration and data analysis.


### Data exploration

You would like to begin your analyses with the naep table. You want to make sure you know what columns are reported in your data, what the data types are for each column, and what the first few observations look like.

1. Write a query that allows you to inspect the schema of the naep table.
2. Write a query that returns the first 50 records of the naep table.

Another good way to understand your data is by calculating various summary statistics. Summary statistics can give you very useful information like where your data is centered and how spread out it is. These summary statistics include **count**, **average**, **min**, and **max** values.

<ol start="3">
  <li>Write a query that returns summary statistics for <em>avg_math_4_score</em> by state, and sort the results alphabetically by state name.</li>
</ol>

When a state has a large gap between the max and min value for a score, that's a good sign that there may be problems with the education system. You decide that for *avg_math_4_score* a gap of more than 30 between max and min values is an indicator of problems.

<ol start="4">
  <li>Write a query that alters the previous query so that it only returns the summary statistics for avg_math_4_score by state with differences in max and min values greater than 30.</li>
</ol>


### Analyzing your data

Now that you have gathered key insights about your data, you are ready to do some analyses. You would like to report the bottom 10 performing states for *avg_math_4_score* in the year 2000 and the states that scored below the average *avg_math_4_score* over all states in the year 2000.

<ol start="5">
  <li>Write a query that returns a field called <em>bottom_10_states</em> that lists the states in the bottom 10 for <em>avg_math_4_score</em> in the year 2000.</li>
  <li>Write a query that calculates the average <em>avg_math_4_score</em> rounded to the nearest 2 decimal places over all states in the year 2000.</li>
  <li>Write a query that returns a field called <em>below_average_states_y2000</em> that lists all states with an <em>avg_math_4_score</em> less than the average over all states in the year 2000. </li>
</ol>

Think about these things: Did your above lists overlap? Should they overlap? During your analyses, you remember that if missing values are not handled properly, you may end up with inaccurate calculations and incorrect conclusions. In the above lists, you would expect at least some of the same states that showed up in the bottom 10 to also show up as scoring below the average over all states.

<ol start="8">
  <li>Write a query that returns a field called <em>scores_missing_y2000</em> that lists any states with missing values in the <em>avg_math_4_score</em> column of the <em>naep</em> data table for the year 2000. </li>
</ol>


Continuing on with your analyses, you suspect that there may be a correlation between *avg_math_4_score* and *total_revenue* for the year 2000: you hypothesize that where less money is spent, scores will be lower. To rigorously prove something like this would require a rigorous statistical treatment, but for now you can write a query that should allow you to "eyeball" this correlation.

<ol start="9">
  <li>Write a query that returns for the year 2000 the state, avg_math_4_score, and total_expenditure from the naep table left outer joined with the finance table using id as the key and ordered by total_expenditure greatest to least. Be sure to round avg_math_4_score to the nearest 2 decimal places and then filter out NULL avg_math_4_scores in order to more clearly determine a correlation.</li>
</ol>

You should see that — at first glance — there seems to be a correlation.
