---
layout: post
title:  "Webscraping Sports Reference with R"
date:   2022-09-20
author: Tyler Ward
description: How to use the rvest library to collect data for all your favorite sports
image: /assets/images/rvest.png
---

# Webscraping Sports Reference with R in 5 easy steps


![Cool Mountain Image Peaked](https://raw.githubusercontent.com/runstats21/stat-386-projects/main/assets/images/sean-martin-PgZ4WfREKZk-unsplash.jpg)
<br>

Up-to-date sports data can be found among the webpages of [sportsreference.com](https://www.sports-reference.com/) for several of the worlds most popular sports, from (college football) to (hockey) and from (baseball) to (soccer). This data, once accessed, can be used to build a variety of fascinating machine learning models to provide insights into performance analysis, scouting and draft projections, and game win prediction (see examples [here](http://vision.lmi.link/docs/janezp/Pers-ereview2000.pdf), [here](https://github.com/runstats21/rb-draft-model), and [here](https://github.com/gschwaeb/NHL_Game_Prediction))


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



### 2. Identify HTML characteristics of webpage

Before applying rvest functionality to scrape a webpage's data, you need to familiarize yourself

In order to find HTML structure of your webpage, using `Ctrl + Shift + C` (`Command + Shift + C` for Mac users)

(Insert screen shot here)
<img width="958" alt="image" src="https://user-images.githubusercontent.com/112500643/192651156-2932aa55-6304-4144-9d85-d93ae84c8434.png">


Format:


College Football example:
```

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

example:
```
url = "sportsreference.com/cfb/leaders/rb/2021"
map_dfr(url, import_position_data)
```

For more information on webscraping 
