---
layout: post
title:  "Webscraping Sports Reference with R"
date:   2022-09-20
author: Tyler Ward
description: How to use the rvest library to scrape data for all your favorite sports
image: /assets/images/rvest.png
---

# Webscraping Sports Reference with R in 5 easy steps
### A world full of data will end in either greater confusion or great direction, depending on how we used Statistics


![Cool Mountain Image Peaked](https://raw.githubusercontent.com/runstats21/stat-386-projects/main/assets/images/sean-martin-PgZ4WfREKZk-unsplash.jpg)
<br>

### 1. Install and Load Needed Libraries

```
install.packages("tidyverse")
library(tidyverse)
```

OR

```
install.packages("rvest")
library(rvest)
```

Note: *rvest* is already included within the tidyverse, but if you want to access the functions individually, you can load this library on its own.



### 2. Indentify Needed HTML Code and URL


### 3. Scrape html_tables 


### 4. Remove uneeded header rows


### 5. Compile commands as single function for easy use on other pages


### *Bonus Step*: Read in data tables from multiple years/sources and bind theme together using purrr library

After you have created a function, you can use map_dfr() (functionality from the purrr library) to apply the same function to as many urls as possible, and then row bind the output into one data frame.
 
How?
* First, Vectorize the Urls
* Then, Use purrr::map_dfr

**map_dfr**(.x = <vector of urls>, .f = <function name>)

example:
```
url = "sportsreference.com/cfb/leaders/rb/2021"
map_dfr(url, import_position_data)
```


