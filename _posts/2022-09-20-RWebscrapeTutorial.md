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

Up-to-date sports data can be found among the webpages of [sportsreference.com](https://www.sports-reference.com/) for several of the worlds most popular sports, from (college football) to (hockey) and from (baseball) to (soccer). This data, once accessed, can be used to build a variety of fascinating machine learning models to provide insights into performance analysis, scouting and draft projections, and game win prediction (see examples [here](http://vision.lmi.link/docs/janezp/Pers-ereview2000.pdf), [here](https://github.com/runstats21/rb-draft-model), and [here](https://github.com/gschwaeb/NHL_Game_Prediction))


### 1. Install and Load Needed Libraries

In order 

```
install.packages("rvest")
library(rvest)

install.packages("tidyverse")
library(tidyverse) # gives access to pipe operator (%>%), which allows for organized application of functions sequentially within R
```

For more information on the tidyverse and the pipe operator, give [tidyverse.org](https://www.tidyverse.org/) a visit.

### 2. Use Webpage URL to get Webpage HTML elements

Format:
**read_html**(<url of page you want to scrape>) 

College Football example:
```r
 my_url = "https://www.sports-reference.com/cfb/years/2021-rushing.html" # save

 read_html(url)
```

### 3. Identify Webpage Characteristics and Scrape HTML Table(s)

Before applying rvest functionality, it is important to understand the format of the webpage which has the data you want to scrape. Specifically:

* Is the data already grouped into table elements?
* How many tables are there on the webpage?
* Which table(s) on the webpage do you want to scrape?

In order to find HTML structure of your webpage, using `Ctrl + Shift + C` (`Command + Shift + C` for Mac users)

For example, when inspecting [College Football 2021 Rushing Stats](https://www.sports-reference.com/cfb/years/2021-rushing.html) webpage, we can find the table element, as shown in the screenshot below
(Insert screen shot here)
<img width="958" alt="image" src="https://user-images.githubusercontent.com/112500643/192651156-2932aa55-6304-4144-9d85-d93ae84c8434.png">


Format:

Example:
```
 pos_tbl <- read_html(url) %>%
  html_node("table") %>%
  html_table()
 
```


For a more in-depth description of web-page characteristics and HTML, see the dataquest article linked here: [Tutorial: Web Scraping in R with rvest](https://www.dataquest.io/blog/web-scraping-in-r-rvest/)


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
Cover Image: [The Athlytics Blog](https://412sportsanalytics.wordpress.com/2016/11/21/is-nfl-catching-up-with-analytics/)

 
