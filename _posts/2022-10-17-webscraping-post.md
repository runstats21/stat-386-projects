---
layout: post
title:  "College Scoreboard: Accessing Higher Education Statistics with US Department of Education API"
date:   2022-10-17
author: Tyler Ward
description: Education is powerful. This post outlines how to collect data on thousands of Higher Education institutions nationwide.
image: /assets/images/US-dept-ed-seal.png
---


# Introduction

Since the onset of the COVID-19 pandemic, college enrollment in the US has declined for [three years straight](https://www.washingtonpost.com/education/2022/10/20/college-enrollment-declines-since-pandemic/) (as reported by the [Washington Post](https://www.washingtonpost.com/education/2022/10/20/college-enrollment-declines-since-pandemic/)), even with access to information greater than ever before. For both parents and young adolescents, many factors contribute to the decision to enroll in college, and to which institution(s) to enroll, including enrollement size, admission rates, and income after graduation. 

Fortunately, the U.S Department of Education has a plethora of data on each of the universities in the United States, that is free for anyone to access after registering for an API key. This data can be used to discover the most desirable colleges in the nation, along with analysis of possible factors leading to a college being "one of the best", such as  ...





Documentation on the College Scorecard and associated API: [College Scorecard Documentation](https://collegescorecard.ed.gov/data/documentation/)

[Brigham Young University](https://www.linkedin.com/school/brigham-young-university/mycompany/verification/)
![BYU](https://user-images.githubusercontent.com/112500643/196997715-79f57fe4-b6ac-489a-aff0-571d9d9384fd.png)




*Complete code for this data collection can be found in [this GitHub repo]*(https://github.com/runstats21/college-score-card-analysis)


# Data Collection

## Tools

[Python's Requests Library](https://realpython.com/python-requests/)

<img width="750" alt="image" src="https://user-images.githubusercontent.com/112500643/197099386-b8dd41cb-7bcf-4046-913a-e8d923196354.png">

Using the [requests module](https://pypi.org/project/requests/) within Python, I was able to obtain valuable information on almost 2000 University's throughout the U.S. via the College Scoreboard government API. However, any resource that allows for API calls will work following a similar process, such as using R's [httr](https://httr.r-lib.org/) and [jsonlite](https://www.rdocumentation.org/packages/jsonlite/versions/1.8.2) packages.




Additionally, as I was working to collect desirable data from the API, I found a suburbly helpful [GitHub repos](https://github.com/kiseki1107/College-Scorecard-Data-Analysis) from [Clarence Li (kiseki1107)](https://github.com/kiseki1107) which outlined the keys he used to get desired data values from the API. I used his framework for my own data collection, outlined in more detail in Step 3 below.


## Step 1: Optain API URL and API key 

A simple search for "College Scoreboard API" will direct you to data documentation for the Department of Education's free API. Specified there is the url location of the API **http://api.data.gov/ed/collegescorecard/**, and the endpoint for querying all data **/v1/schools**.

```python
# base url
url = "http://api.data.gov/ed/collegescorecard/v1/schools?" # question mark will allow for (optional) arugments to be appended
```

After saving this url you can register for an API key, which will promptly be sent to you via email.

<img width="956" alt="image" src="https://user-images.githubusercontent.com/112500643/197102279-684b1f1f-14a1-43b3-bdc0-64a0f13c4834.png">



## Step 2: Prepare API key for GitHub

## Step 3: Identify field parameters of interest

## Step 4: Gather corresponding data of interest

## Step 5: Data Cleaning of Percent variables


**My data:**

<img width="665" alt="image" src="https://user-images.githubusercontent.com/112500643/197097649-cdd0b9df-0c72-4da5-8c99-249a1f13e6a0.png">


# Conclusion

This is what I did!

**Call** to action



