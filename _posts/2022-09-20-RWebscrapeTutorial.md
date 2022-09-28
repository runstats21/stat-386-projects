---
layout: post
title:  "Webscraping Sports Reference with R in 5 easy steps"
date:   2022-09-20
author: Tyler Ward
description: How to use the rvest library to collect data for all your favorite sports
image: /assets/images/nfl-analytics.png
---

# Webscraping Sports Reference with R in 5 easy steps
### Always wanted to get data about your favorite sport for an innovative statistical model? This tutorial is your place to begin 

<br>

Up-to-date sports data can be found among the webpages of [sportsreference.com](https://www.sports-reference.com/) for several of the worlds most popular sports, from (college football) to (hockey) and from (baseball) to (soccer). This data, once accessed, can be used to build a variety of fascinating machine learning models to provide insights into performance analysis, scouting and draft projections, and game win prediction (see examples [here](http://vision.lmi.link/docs/janezp/Pers-ereview2000.pdf), [here](https://github.com/runstats21/rb-draft-model), and [here](https://github.com/gschwaeb/NHL_Game_Prediction)).

This tutorial explains how to webscrape data from a sports reference web page in 5 easy steps, along with a bonus step on how to scrape and combine data from multiple web pages into one data frame.

### 1. Install and Load Rvest and Tidyverse packages

In order to scrape data from a webpage in R, you will need to install and load the `rvest` package. Additionally, this tutorial uses a pipe operator to steamline the scraping process, which can be accessed by installing and loading the `tidyverse` library. If you already have the rvest and tidyverse packages installed, you do not need to install them again. 

```r
# install packages, as applicable
install.packages("rvest")
install.packages("tidyverse")

# load rvest and tidyverse libraries
library(rvest)
library(tidyverse)
```

A tutorial on webscraping in R without using the tidyverse can be found [here](https://www.geeksforgeeks.org/web-scraping-using-r-language/).
For more information on the tidyverse and the pipe operator, give [tidyverse.org](https://www.tidyverse.org/) a visit.

For more information on the tidyverse and the pipe operator, give [tidyverse.org](https://www.tidyverse.org/) a visit.

### 2. Use Webpage URL to get Webpage HTML elements

Format:
**read_html**(url of page you want to scrape) 

College Football example:
```r
 my_url = "https://www.sports-reference.com/cfb/years/2021-rushing.html" # save url as R object

 read_html(my_url) # read html from my_url
```

### 3. Identify Webpage Characteristics and Scrape HTML Table(s)

Before applying rvest functionality further, it is important to understand the format of the webpage which has the data you want to scrape. Specifically:

* Is the data already grouped into table elements?
* How many tables are there on the webpage?
* Which table(s) on the webpage do you want to scrape?

In order to find HTML structure of your webpage, using `Ctrl + Shift + C` (`Command + Shift + C` for Mac users)

For example, when inspecting the following [College Football 2021 Rushing Stats](https://www.sports-reference.com/cfb/years/2021-rushing.html) webpage, we can find the table element:
<br>

<img width="959" alt="image" src="https://user-images.githubusercontent.com/112500643/192863594-de3548c5-09e8-49aa-b7fc-8f1555dd6433.png">
 
The webpage in this example has only one table, so we can scrape this data table quite easily by telling R to get the "table" html element, using the function `html_element()`
 
Format:
 **html_element**(read-in webpage html, "element to access")

Example:
 
```r
 read_html(url) %>%
  html_element("table") %>%
  html_table()
 
```

If a webpage has more than one table, simply apply the `html_elements()` function in place of `html_element()`, which will import each of the desired tables as a list. You can then access your desired table by calling the corresponding list element. For example, if you want to get the first table from the webpage, use `.[[1]]`, as shown in the example below.

```r
 read_html(my_url) %>%
  html_elements("table") %>% # get all table elements on webpage and combine them into a list
  html_table() %>%
  .[[1]] # get first table
```

For a more in-depth description of web-page characteristics and HTML, see the opening sections of the dataquest article linked here: [Tutorial: Web Scraping in R with rvest](https://www.dataquest.io/blog/web-scraping-in-r-rvest/)


### 3. Scrape html_tables 


### 4. Remove uneeded header rows


### 5. Compile commands as single function for easy use on other pages


### *Bonus Step*: Read in data tables from multiple years/sources and bind theme together using purrr library

After you have created a function, you can use map_dfr() (functionality from the purrr library) to apply the same function to as many urls as possible, and then row bind the output into one data frame.
 
How?
* First, Vectorize the Urls
* Then, Use purrr::map_dfr

**map_dfr**(.x = <vector of urls>, .f = <function name>)

example (using the function created in step 5 above):
```
 url = "sportsreference.com/cfb/leaders/rb/2021"
 map_dfr(url, import_position_data)
```

### **Acknowledgements**
 
* Cover Image: [The Athlytics Blog](https://412sportsanalytics.wordpress.com/2016/11/21/is-nfl-catching-up-with-analytics/)
* Complete rvest documentation: https://www.rdocumentation.org/packages/rvest/versions/1.0.3

 
