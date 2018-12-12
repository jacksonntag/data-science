---
title: Cleaning data
author: Thinkful
team: grading
time: 60
uuid: c8ef5497-a29a-4d16-88bf-ac49fb4e3be5
---

In this lesson we'll cover how to identify and correct many types of "dirty" data.

## Finding dirt

In a data scientist's paradise, all data arrive clean and analyses can start right away.  In reality, data is often dirty and requires some processing first.  Data is "dirty" if it contains irrelevant or misleading information.  Finding dirt can be hard. Some types of dirty data are only identifiable as dirty if you know something about how the data was collected.  For example, a histogram of a variable with values between 0 and 7 may look perfectly normal and seem fine… unless you know that the variable in question is only supposed to have values between 1 and 7.  Codebooks and metadata are a great resource for data cleaning; view datasets without these with suspicion.  Visualizations are an excellent tool for identifying dirty data. You can also take a look at a sample of the raw data file, to get a sense of what typical values look like.

## Cleaning dirt

If data is dirty, then it must be cleaned before analysis.  Cleaning involves removing the problematic values and, potentially, replacing them with other, less problematic versions.

### Replace with a missingness indicator (`None` in Python, `NULL` in SQL):

**Anomalous values**

 * A variable is supposed to range between 1 and 7, but you see a "99".
 * A height in inches variable lists someone's height as "100".
 * A write-in age variable includes entries such as "old enough" and "29999".

**Fake answers**

 * A person answers "a" to every question ("**straightlining**"").
 * Answers form a repeating pattern: "1, 2, 3, 4, 1, 2, 3, 4, 1, 2, 3, 4".
 + Plotting data can sometimes guide by showing what **normal responses** look like.
 * Time from start to finish of a task is less than an established threshold (10 seconds, 30 seconds, etc) suggesting the person did not follow the task instructions.
 + **Plotting** the response time distribution can help to find a logical cutoff point.

### Map to a valid response:

 **Anomalous values**
 * If a scale goes from 1 to 7 and one answer is 77, it _may_ be acceptable to change the answer to 7. If you suspect the wrong units are being used (a variable asks for height in inches, someone fills in "6"), it _may_ be acceptable to convert to the correct units.

 **Extreme but plausible values**
 * A person in a random sample reports a height of "7 feet" and an annual income of "$20 Million".
 * Response rates for ads in one city are three times as high as response rates in all other cities.

 One popular approach  to extreme but plausible values is to **replace** the valid but extreme values with the highest non-outlier value. This retains information (a 7-foot-tall person is quite tall relative to the majority of the sample) while getting rid of the undesirable effects of an outlier.  The "highest non-outlier" value can be identified in various ways.  One method, "[winsorizing](https://en.wikipedia.org/wiki/Winsorizing)", chooses a percentile such as 90% and assigns all values below the 5th percentile equal to the value at the 5th percentile, and all values above the 95th percentile to the value of the 95th percentile.   

### Remove:

**Duplicate entries**

 * A user submits a form twice.
 * Two data sources are combined and include some overlap.

### Other:
Some forms of data cleaning require _major_ judgment calls because the "dirty" pattern is widespread and/or systematic.  Missing data, for example, can make a dataset dirty if you suspect that there is a data-related reason why those particular values are missing.  For example, low-income survey respondents may systematically skip the "income" question, while higher-income respondents are less likely to skip it.  Without some kind of cleaning or correction, this will cause the average income of the sample to appear higher than it truly is.  Missing data correction is sufficiently complex to be covered in its own assignment within this lesson.


<div class= think-like-a-data-scientist>
<p><em>Never</em> clean data by modifying the datafile by hand.  Always do data cleaning programmatically, even if you are only replacing one value in one cell with another value.  This will guarantee that you have a record of everything you've done. Since data cleaning changes the data, different data cleaning decisions will have different effects on what the analyses will say, so it is vital to keep a record.</p>

<p>In general, treat raw data files as though they were chiselled on stone tablets, never to be changed.  Never overwrite them with a cleaned file.  Ideally, you won't have a "clean" file at all, but instead a 'cleaning' script that you'll call each time you work with the data.  This ensures that you always know exactly what has been done to create the datafile you're analyzing.</p>
</div>

### Summary

Data cleaning is a vitally important step in the data science process.  Without cleaning, the best modeling and interpretation in the world is vulnerable to "GIGO": Garbage In, Garbage Out.  The best cleaning involves intensive plotting of the raw data by someone who knows how and why the data was collected and what sorts of values are expected.