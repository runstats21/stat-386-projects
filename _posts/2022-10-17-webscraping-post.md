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

Fortunately, the U.S Department of Education has a plethora of data on each of the universities in the United States, that is free for anyone to access after registering for an API key. This data can be used to discover the most desirable colleges in the nation, and will also allow for analysis of the reltionships between different college statistics, such as the relationship between faculty salary and student income 6 years after entry, or between admission rate and completion rate.

[College Scorecard Documentation](https://collegescorecard.ed.gov/data/documentation/)

A later post will outline exploratory analysis and insights from this dataset to be able to understand key factors in top tier higher education, and which universities qualify as "the top" schools in the nation.

[Brigham Young University](https://www.linkedin.com/school/brigham-young-university/mycompany/verification/)
![BYU](https://user-images.githubusercontent.com/112500643/196997715-79f57fe4-b6ac-489a-aff0-571d9d9384fd.png)


*Complete code for this data collection can be found in [this GitHub repo]*(https://github.com/runstats21/college-score-card-analysis)


# Data Collection

## Tools

[Python's Requests Library](https://realpython.com/python-requests/)

<img width="750" alt="image" src="https://user-images.githubusercontent.com/112500643/197099386-b8dd41cb-7bcf-4046-913a-e8d923196354.png">

Using the [requests module](https://pypi.org/project/requests/) within Python, I was able to obtain valuable information on almost 2000 University's throughout the U.S. via the College Scoreboard government API. However, any resource that allows for API calls will work following a similar process, such as using R's [httr](https://httr.r-lib.org/) and [jsonlite](https://www.rdocumentation.org/packages/jsonlite/versions/1.8.2) packages. As noted on the College Scorecard website, this data is free and easily accessible by anyone. 

As I was working to collect desirable data from the API, I found an extremely helpful [GitHub repos](https://github.com/kiseki1107/College-Scorecard-Data-Analysis) from [Clarence Li (kiseki1107)](https://github.com/kiseki1107) which outlined the keys he used to get desired data values from the API. I used his framework for my own data collection, outlined in more detail in Step 3 below.

Steps for collecting data from this wonderful resource are outlined below.


## Step 1: Optain API URL and API key 

A simple search for "College Scoreboard API" will direct you to data documentation for the Department of Education's free API. Specified there is the url location of the API **http://api.data.gov/ed/collegescorecard/**, and the endpoint for querying all data **/v1/schools**.

```python
# base url
url = "http://api.data.gov/ed/collegescorecard/v1/schools?" # question mark will allow for (optional) arugments to be appended
```

After saving this url you can register for an API key at the bottom of the page (see image below), which will promptly be sent to you via email. 

<img width="956" alt="image" src="https://user-images.githubusercontent.com/112500643/197102279-684b1f1f-14a1-43b3-bdc0-64a0f13c4834.png">

Look for an email with subject "Your API Key", from noreply@api.data.gov. *Be sure to check your junk mail if it cannot be found in your normal inbox!*


## Step 2: Prepare API key for GitHub

In order to share the code for data collection without comprimising my API key, I needed to:

* Paste and save the API key into a text file (e.g., "apikey.txt"
* Add the text file name to my .gitignore file, e.g.:

```
apikey.txt
```

* Move the text file into my working directory and save it as an object in my Jupyter Notebook

```python
# load and save api_key
with open('apikey.txt', 'r') as file:
    apikey = file.read()
```



## Step 3: Identify field parameters of interest

With the base url ready, I used `requests.get()` function to extract data from the API.

To extract desired data variables from the json file, the correct listings on the dictionary must be specified. For example, the following dictionary, which I used, allows for extraction of 40 different variables related to School, Cost, Admission, and Earnings.

```python
# Dictionary of all desired fields
year = "latest" # get latest data
fields = {
      # School Category
      "School Name": "school.name",
      "School ID": "id",
      "School State": "school.state",
      "School Ownership": "school.ownership",
      "Full-time Faculty Rate (%)": "school.ft_faculty_rate",
      "Faculty's average salary per month": "school.faculty_salary",
      # Student Category
      "Student Enrollment Size": year + ".student.size",
      "Student Enrollment All": year + ".student.enrollment.all",
      "Male Students (%)": year + ".student.demographics.men",
      "Female Students (%)": year + ".student.demographics.women",
      "Retention Rate 4 Yr (%)": year + ".student.retention_rate.four_year.full_time",
      # Cost Category
      "Attendance Cost per Academic Year": year + ".cost.attendance.academic_year",
      # Completion Category
      "150% Completion Rate at 4 Yr (%)": year + ".completion.completion_rate_4yr_150nt",
      # Admissions Category 
      "Admission Rate (%)": year + ".admissions.admission_rate.overall",
      "SAT Average Overall": year + ".admissions.sat_scores.average.overall",
      "SAT 75th Percentile Critical Math": year + ".admissions.sat_scores.75th_percentile.math",
      "SAT 75th Percentile Critical Reading": year + ".admissions.sat_scores.75th_percentile.critical_reading",
      "SAT 75th Percentile Critical Writing": year + ".admissions.sat_scores.75th_percentile.writing",
      ## Earnings Category
      # 6 Years after Enrollment:
      "Mean Earnings (6 Yrs after Entry)": year + ".earnings.6_yrs_after_entry.working_not_enrolled.mean_earnings",
      "Mean Male Earnings (6 Yrs after Entry)": year + ".earnings.6_yrs_after_entry.mean_earnings.male_students",
      "Mean Female Earnings (6 Yrs after Entry)": year + ".earnings.6_yrs_after_entry.mean_earnings.female_students",
      "Std. Deviation Earning (6 Yrs after Entry)": year + ".earnings.6_yrs_after_entry.working_not_enrolled.std_dev",
      "Percent of Students Earning >$25K (6 Yrs after Entry)": year + ".earnings.6_yrs_after_entry.percent_greater_than_25000",
      "Low Income Students (6 Yrs after Entry)": year + ".earnings.6_yrs_after_entry.working_not_enrolled.income.lowest_tercile",
      "Medium Income Students (6 Yrs after Entry)": year + ".earnings.6_yrs_after_entry.working_not_enrolled.income.middle_tercile",
      "High Income Students (6 Yrs after Entry)": year + ".earnings.6_yrs_after_entry.working_not_enrolled.income.highest_tercile",
      "Mean Earnings Low (6 Yrs after Entry)": year + ".earnings.6_yrs_after_entry.mean_earnings.lowest_tercile",
      "Mean Earnings Medium (6 Yrs after Entry)": year + ".earnings.6_yrs_after_entry.mean_earnings.middle_tercile",
      "Mean Earnings High (6 Yrs after Entry)": year + ".earnings.6_yrs_after_entry.mean_earnings.highest_tercile",
      # 10 Years after Enrollment:
      "Mean Earnings (10 Yrs after Entry)": year + ".earnings.10_yrs_after_entry.working_not_enrolled.mean_earnings",
      "Mean Male Earnings (10 Yrs after Entry)": year + ".earnings.10_yrs_after_entry.mean_earnings.male_students",
      "Mean Female Earnings (10 Yrs after Entry)": year + ".earnings.10_yrs_after_entry.mean_earnings.female_students",
      "Std. Deviation Earning (10 Yrs after Entry)": year + ".earnings.10_yrs_after_entry.working_not_enrolled.std_dev",
      "Percent of Students Earning >$25K (10 Yrs after Entry)": year + ".earnings.10_yrs_after_entry.percent_greater_than_25000",
      "Low Income Students (10 Yrs after Entry)": year + ".earnings.10_yrs_after_entry.working_not_enrolled.income.lowest_tercile",
      "Medium Income Students (10 Yrs after Entry)": year + ".earnings.10_yrs_after_entry.working_not_enrolled.income.middle_tercile",
      "High Income Students (10 Yrs after Entry)": year + ".earnings.10_yrs_after_entry.working_not_enrolled.income.highest_tercile",
      "Mean Earnings Low (10 Yrs after Entry)": year + ".earnings.10_yrs_after_entry.mean_earnings.lowest_tercile",
      "Mean Earnings Medium (10 Yrs after Entry)": year + ".earnings.10_yrs_after_entry.mean_earnings.middle_tercile",
      "Mean Earnings High (10 Yrs after Entry)": year + ".earnings.10_yrs_after_entry.mean_earnings.highest_tercile"
     }
    
# Appending all the fields values together into one "fields_url"
fields_url = ""
for key, val in fields.items():
    fields_url = fields_url + val + ","

# To remove the extra "," at the end of fields_url
fields_url = fields_url[:-1]
fields_url
```



## Step 4: Gather corresponding data of interest



## Step 5: Data Cleaning of Percent variables


**My data:**

<img width="665" alt="image" src="https://user-images.githubusercontent.com/112500643/197097649-cdd0b9df-0c72-4da5-8c99-249a1f13e6a0.png">


# Conclusion

This is what I did!

In the next post I will perform analysis outlining interesting relationships between the myriad of college statistics now contained in my dataset. In the mean time, I challenge you to collect your own data from the College Scorecard API, and give me feedback on any issues you run into, and prepare to analyze the data yourself!




