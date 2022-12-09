---
layout: post
title:  "Come and Stay: College Retention Rates in the United States"
date:   2022-12-08
author: Tyler Ward
description: What factors contribute to student retention at U.S. colleges? This post examines two key factors based on data from the Department of Education's College Scorecard
image: /assets/images/stanford.jpg
---

![su-puloo-GBVZyAWf014-unsplash](https://user-images.githubusercontent.com/112500643/206622042-6354f947-2ebc-4d70-bda7-45f74e0ecd57.jpg)

Photo by <a href="https://unsplash.com/@supuloo?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Su puloo</a> on <a href="https://unsplash.com/s/photos/Brigham-Young-University?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>


# College Scorecard Analysis

About a month ago I began analysis of data from approximately 2000 colleges and universities in the United States of America. These data are publicly available and are updated regularly by the U.S Department of Education. Using their specified [College Scorecard](https://collegescorecard.ed.gov/data/documentation/) API, I was able to collect 40 different data points for each of approximately 2000 four-year bachelors degree awarding colleges nationwide. I then completed exploratory analysis of several of the collected variables, including many graphics produced with Python's [seaborn](https://seaborn.pydata.org/) and [plotly express](https://plotly.com/python/plotly-express/) packages.

## Data Story

{% include final_figure.html %}

## GitHub Repository

Full code for this graphic and my whole analysis (data collection, EDA, and interactive graphics) can be found at my [College Scorecard Analysis](https://github.com/runstats21/college-score-card-analysis) GitHub repository [here](https://github.com/runstats21/college-score-card-analysis).

## Moving Forward

I'm excited to continue analysis of these data as it is updated through the coming months and years including production of predictive models to better understand and predict meaning metrics of sucessful universities such retention rates. In the mean time, I invite you to share your thoughts with me on in the comments below and don't hesitate to reach out over Linkedin to connect further.
