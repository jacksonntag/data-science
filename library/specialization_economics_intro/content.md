---
title: Intro
author: Thinkful
team: grading
time: 90
uuid: da5b8701-bc15-444a-9c7b-c7091194b8db
---

For a large portion of this course, we’ve focused on robust machine learning algorithms that do a fantastic job predicting or modeling outcomes with high degrees of accuracy for a wide variety of problems. Our goal is usually to craft the system that produces the most accurate results, typically based around some single or set of metrics.

However, not all fields have approached data with those same priorities. Specifically, Economics (as well as other social sciences) have developed their own approach to data, combining some classic techniques with contemporary scale. This specialization handles those topics.

We'll outline an approach to the data and data science behind markets, production, consumption, wealth, and employment. This is an enormously broad range of topics, a few of which we've selected to introduce you to the field. Some problems focus on data aggregated at the national or global level, while others focus on the behaviors of individuals. These problems have their own typical approaches and there are modules of the course so far (as well as other specializations) that will be particularly relevant.

## Data sources

The distinguishing feature of an economics problem is often the data itself. Economics tends to work with relatively specialized data sources that are often publicly available and collected or reported by government bodies or agencies. As such, one key to being a data scientist in this area is to be familiar with these data sources.

We will use this assignment to introduce a few such data sources, explaining some of their significance and interesting features. As a note, this assignment will focus on data from first-world countries in the Western Hemisphere, but similar resources exist for many other countries (getting data about less developed countries, however, can be much harder and less reliable).

This page may be useful to refer back to should you wish to create an economics focused capstone.

### [FRED](https://fred.stlouisfed.org/)

If there was a data apocalypse and only one data source was to survive, many economists would likely choose FRED. FRED stands for Federal Reserve Economic Data, and while it contains the Federal Reserve in its title, the data actually comes from over 80 different sources and departments. All told, there are over 450,000 data sets on this site, covering a range of topics from inflation to GDP to employment. 

If there is a measure of the US economy in aggregate over time, chances are, it's in FRED.

### [ICPSR](https://www.icpsr.umich.edu/icpsrweb/)

ICPSR, or the Interuniversity Consortium for Political and Social Research, housed at the University of Michigan, is another fantastic source for economic data, popular with economists, sociologists, psychologists, political scientists, and others. There is a lot of economic data here, and a wide variety of studies that can perhaps best be described as... obscure. 

Want data for arrests in Paris in June 1848? This is your place. Heights of French soldiers in 1716-1784? Done. American Symphony Orchestra Repertoires from 1842-1970. Boom.

Point is, if you ask yourself 'I wonder if this data exists...' this may be a good place to look.

### Government and Intergovernmental Websites

Governments publish an incredible amount of data, and while much of it gets aggregated to sites like ICPSR or FRED, there are a few departments worth particular attention to if you're working within the field of Economics.

First, the _Bureau of Labor Statistics_ has a wealth of economic information. They produce information on compensation, pricing, and consumption, with possibly their most valuable dataset coming in the form of the _[Consumer Expenditure Survey](https://www.bls.gov/cex/)_ (sometimes abbreviated CEX). This is a fantastically valuable survey containing information about the consumption, income, and demographics of individuals in the US. This is also what's called a _panel dataset_, containing data for individuals over multiple time periods (in this case five consecutive quarters).

Another survey worth giving particular mention is the _[American Community Survey](https://www.census.gov/programs-surveys/acs/)_, conducted by the US Census Bureau, is of particular interest. This gives information about demographics and communities, which is useful for understanding how cities and areas are changing.

There are many more economic data sources, with Yale's Law Library having put together a more extensive [collection](http://library.law.yale.edu/news/75-sources-economic-data-statistics-reports-and-commentary) of other sources.

### Financial Markets Data

For economists, good source of data is financial markets data. While this a dangerous assumption, financial markets are often used as a proxy for economic health or sentiment. The nice thing about this data is that it is incredibly detailed and rich.

The data is readily and consistently available, giving you a well maintained time series for this information. You can find some domestic stock market indices on FRED, as well as on financial aggregator sites like [Barrons](http://www.barrons.com/data).

Before moving on, make sure you take some time to actually go out and explore at least a few of these sites. Familiarity with what's available will help you see what's possible when the time comes to build your capstone.


## Production economics

One fundamental branch of economics if the economics of production, or how things are made. Now, when economics thinks about production they aren't really thinking about how many screws it takes to put together a table or something like that, but rather what larger inputs combine to create goods and how changing those will impact the amount produced.

We'll explain with an example.

### Economic Production

Think about the table for a second. Let's say the table is made of two things: pieces of wood and screws. More specifically, it takes 10 pieces of wood and 4 screws to make a table. If you have 10 pieces of wood and 3 screws no table. 11 pieces of wood and 4 screws, and you still just produce one table.

This production problem has a fixed ratio of inputs. Every table takes 10 pieces of wood and 4 screws. Additional resources make no difference until you reach enough to make a whole new table.

This is not a particularly interesting production problem, and there isn't much optimization to be done here. Things are pretty fixed. However, let's think about something else.

Think about salespeople and products, trying to manufacture sales.

If you have 10 salespeople and 20 products, perhaps you generate 14 sales. However, maybe an additional salesperson adds just one additional sale. Maybe carrying more inventory increases sales, but not at the same proportion as some things sit on the shelves. The ratio here is not necessarily fixed, and those returns to scale are a challenge to model.

This is a much more challenging data problem, and economics and data science give us tools to deal with it.

### Cobb-Douglas Production

One of the archetypal formulae of economics is the _Cobb-Douglas Production Function_. This function gives us the relationship between two inputs and their production.

Specifically:

$$ Y = AL^BK^a $$

Here, Y is the total output produced. A is a factor of productivity, scaling the output appropriately. L and K are our two inputs, classically exemplified by labor and capital, though this production function has broader implications. Beta and alpha are our two output elasticities, helping to quantify the effect of additional units of our inputs on the output.

This function has several convenient mathematical attributes. Firstly, both units of production (the L and the K) feature diminishing marginal returns. What this means is each additional unit produces decreased output.

It also allows for varied forms of returns to scale. If the sum of our two exponents is less than 1, we see decreasing returns to scale. This means if we multiply our inputs by some factor, say 2, our outputs increase by less than that factor. If the exponents sum to 1, we have constant returns of scale (multiply inputs by 2, output increases 2 fold). Lastly, if they some to more than one, we have increasing return to scale (you guessed it, multiply inputs by 2, output increases by more that 2 times).

### How can we use this?

So how do we use this function to our advantage? We can use linear regression! Specifically, if we expect this relationship might be playing out in our data, we can use logs to transform it into a linear regression. Specifically, take the log of each side of the equation, utilizing the properties of logs, specifically log(xy) = log(x) + log(y) and log(x^a) = alog(x). (If you’re unfamiliar with log math you can get a quick refresher [here](https://en.wikipedia.org/wiki/Logarithm#Logarithmic_identities).

We get:

$$ log(Y) = c + Blog(L) + alog(K)

If we transform our Y, L, and K into their respective logs, we can place them into a linear regression and our coefficients will estimate the values of beta and alpha.

### Where do we use this?

This can be used for any kind of production we're working with. It could be trying to model the production of a good from labor and raw materials. It could be about sales from marketing and inventory spend. If it has limited, easily countable inputs, we can try this approach. If the model fits reasonably well, we know more about the relationship of production and can use that to help better formulate how to grow production.


## Models

So how does economics approach modeling?

The primary tool used is one you've seen before: Linear Regression. Now, as we've also seen throughout the Supervised Learning section of the course, there are many varieties of linear regression that exist. Specifically we've already covered OLS, logistic, lasso, and ridge regression. But there are many other forms of regression out there, and some of them are particularly useful for economic data.

But first...

### Why linear regression?

We've already explained linear regression, but as we said most of the time it isn't the most accurate form of predictive model. There are things we can do to make it more accurate, but still, why would a discipline have such a clear and apparent preference for one less-than-optimal class of model?

The reason is explanatory power. Economists are rarely invested in just predicting something with little or no explanation. They want to understand why things are happening and how we can affect the outcome. That gives linear regression a powerful advantage. These models are highly interpretable. We can take our coefficients and understand what they mean. We can compare the coefficients if we run our model in one circumstance and again in another.

Economics also often deal with aggregate data (think things like unemployment rate or GDP) where the data sets can be too small for other techniques to be stable or reliable.

That said, economists do not limit themselves to simple linear regression. In addition to the techniques we covered in advanced regression, there are a few others worth being familiar with.

### Robust Regression

Robust Regression is a useful data science tool and is particularly common in economics. It is useful when you have outliers in your data that you want to prevent from dominating your model. By that we mean that a set of outliers can have a very strong influence on a linear model's coefficient because their errors are so large. These errors can also lead to volatility in your coefficients, another undesirable outcome, particularly if your goal is for those coefficients to be interpretable.

Robust Regression gives you a way to handle this. `Sci-kit Learn` supports three different varieties of Robust Regression: Huber, Thiel-Sen, and RANSAC. These all work differently and better in different circumstances. Huber, for example, works particularly well when the outliers are in the response or outcome, rather than the input variables. Something like Thiel-Sen will work better with errors in inputs. RANSAC tends to work best if the outliers are large.

Briefly, these three models work as follows:

RANSAC stands for RANdom SAmple Consensus. This iteratively works through several random samples of the data to build linear regression models and then searches for outliers (based on their errors). 

Thiel-Sen relies on medians, rather than assuming a normally distributed error, which makes outliers irrelevant (unless there are enough of them to shift the median).

Huber uses a loss function on outliers, meaning the further out they are the less they influence the regression (though they do still influence it).

You can either know which kind of regression you want to use or try all three and see which one works the best (which is, quite honestly, what most people do).


### Probit and Tobit

Probit and tobit are two totally different spins on the linear regression framework, but they sound similar so we'll group them together.

Probit models a probabilistic outcome, so it is used for the same kind of problems as logistic regression. This cuts off our outcomes at 1 and 0, forcing the outcome to be within those probabilistic bounds (something standard linear regression would not do). This bounding of our output makes it so the outputs of the model are generally valid, rather than capable of producing impossible outcomes in edge cases..

Tobit can be thought of as a positives only linear regression. This is done through a linear regression whose coefficient is then reinterpreted such that all negative outcomes are associated with zero. Again, this ensures that the output is always valid should negative values be illogical or impossible.

Lastly, sometimes logistic regression will get called 'logit', just to complete the group of regression models with the same structure to their name.

### STATA 

Before we stop talking about economic modeling, we have to mention STATA. Many economists do not use Python. They do not use R. They use STATA.

There are several reasons we're not using STATA in this course.

Firstly, it's more of a scripting language than a programming language. It will let you manipulate data a little bit but is nowhere near as powerful nor as adaptable as python.  It is also not open source and therefore not free. It can be expensive to maintain an up to date version of STATA, with new releases requiring new purchases.However, it does give extensive output on the fit of your models (though it is limited to certain classes of model) and is incredibly easy to write for.

If you end up working in economics or in economic research (or plenty of other social sciences) you may see STATA. Provided you're familiar with the fundamentals of how linear models work, it shouldn't provide much of an impediment to getting work done, and you should be able to do what you need to.

