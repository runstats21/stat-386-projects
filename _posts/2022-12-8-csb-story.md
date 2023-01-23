---
layout: post
title:  "Come and Stay: College Retention Rates in the United States"
date:   2022-12-08
author: Tyler Ward
description: What factors contribute to student retention at U.S. colleges? This post examines two key factors based on U.S. Department of Education College Scorecard data
image: /assets/images/stanford.jpg
---

![su-puloo-GBVZyAWf014-unsplash](https://user-images.githubusercontent.com/112500643/206622042-6354f947-2ebc-4d70-bda7-45f74e0ecd57.jpg)

Photo by <a href="https://unsplash.com/@supuloo?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Su puloo</a> on <a href="https://unsplash.com/s/photos/Brigham-Young-University?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>


# College Scorecard Analysis

About a month ago I began analysis of data from approximately 2000 colleges and universities in the United States of America with the desire to understand more about what makes a college successful and which U.S. colleges are succeeding in helping students complete college and be successful in the years beyond. Data for each university in America are publicly available from a database updated regularly by the U.S Department of Education. Using their specified [College Scorecard](https://collegescorecard.ed.gov/data/documentation/) API, I was able to collect 40 different data points for each of approximately 2000 four-year bachelors degree awarding colleges nationwide. The cleaned data is readily available on my GitHub [here]. I then completed exploratory analysis of several of the collected variables, including many graphics produced with Python's [seaborn](https://seaborn.pydata.org/) and [plotly express](https://plotly.com/python/plotly-express/) packages . This analysis led me to many findings, including intriguing relationships between variables like average faculty salary, SAT scores, and admission rates with college retention rates and earnings of students 10 years after university entry. 

Each of these findings let me to dig deeper into the data and build interactive graphs to quickly look at many different relationships in a clear and concise way. After examining many variables, the relationship between both SAT scores and faculty salary with student retention rate caught my attention, which led me to create the graphic below along with several others. Code for each piece of my analysis can be found at my [Github repository](https://github.com/runstats21/college-score-card-analysis) and at the links below:

* [Data Collection](https://github.com/runstats21/college-score-card-analysis/blob/main/CollegeScorecard-CollectClean.ipynb)
* [EDA](https://github.com/runstats21/college-score-card-analysis/blob/main/CollegeScorecardEDA.ipynb)
* [Interactive Graphics](https://github.com/runstats21/college-score-card-analysis/blob/main/CollegeScorecardDataStory.ipynb)

## SAT Scores, Faculty Salary, and Retention Rates

As shown by the graphic below, there appears to be a clear positive relationship between the average faculty salary and the four-year retention rate at U.S universities. Though there are some exceptionally prestiguous universities such as Stanford, Harvard, Princeton and Yale who's retention rates appear lower than most universities relative to the average salary of their faculty, the many universities seem to have retention rates approaching 80 percent when faculty salary is 100 thousand or more on average, with almost all retention rates exceeding 80% as average faculty salary approachs 150 thousand. However, high retention rates seem to be even better explained by SAT Scores. Clearly shown by the orange points, almost all of Top 25% of schools by average overall SAT score have retention rates above 80%, making up most of the 33.74% of bachelor's degree awarding universites with retention rates above 80%. Clear decline of retention rates can be seen for universities at with lower average SAT scores. Therefore, it seems clear that both student preparedness and investment in faculty, as represented by SAT scores and faculty salary, contribute to college four-year retention rates.


{% include final_figure.html %}

## GitHub Repository

Full code for this graphic and my whole analysis (data collection, EDA, and interactive graphics) can be found at my [College Scorecard Analysis](https://github.com/runstats21/college-score-card-analysis) GitHub repository [here](https://github.com/runstats21/college-score-card-analysis).

## Moving Forward

I'm excited to continue analysis of these data as it is updated through the coming months and years including production of predictive models to better understand and predict meaning metrics of sucessful universities such retention rates. In the mean time, I invite you to share your thoughts with me on in the comments below and don't hesitate to reach out over Linkedin to connect further.
