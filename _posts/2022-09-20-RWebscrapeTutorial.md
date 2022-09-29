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

Up-to-date sports data can be found among the webpages of [sportsreference.com](https://www.sports-reference.com/) for several of the worlds most popular sports, from [college football] to [hockey], to [baseball] and [soccer]. This data, once accessed, can be used to build a variety of fascinating machine learning models to provide insights into performance analysis, scouting and draft projections, and game win prediction (see examples [here](http://vision.lmi.link/docs/janezp/Pers-ereview2000.pdf), [here](https://github.com/runstats21/rb-draft-model), and [here](https://github.com/gschwaeb/NHL_Game_Prediction)).

This tutorial explains how to webscrape data from a sports reference web page in 5 easy steps, along with a bonus step on how to scrape and combine data from multiple web pages into one data frame. An example code chunk for scraping college football rushing data will be included with each step, with the full code included at end of this post.

*TO possible do*! :
- change to "Step 1, Step 2, etc.
- add links for pages for each sport
- take out "example"

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

### 2. Use Webpage URL to get HTML elements

After selecting a webpage you want to scrape, save the url as a string object, and use the function `read_html` to read the html from the webpage. You can also access the full html of a web page by using the command `Ctrl + Shift + C` (`Command + Shift + C` for Mac users) while in a web browser.

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

You can identify these characteristics with a quick scroll through of your webpage, along with a `right click + Inspect`. This will open the HTML elements side bar, where you should look for for an element labeled `<table>`. For example, when inspecting the following [College Football 2021 Rushing Stats](https://www.sports-reference.com/cfb/years/2021-rushing.html) webpage, we can find the table element:
<br>

<img width="959" alt="image" src="https://user-images.githubusercontent.com/112500643/192863594-de3548c5-09e8-49aa-b7fc-8f1555dd6433.png">
 
You can then scrape and store this data table by telling R to get the "table" html element from your read-in html, and then convert it into an R data frame. This can be done by simplying piping your read-in html into the functions `html_element()`, asking for the table element in quotation marks, then piping that into the `html_table()` function.
 
```r
data_tbl <- read_html(url) %>% # read html from my_url
  html_element("table") %>% # get first table element
  html_table() # convert table to an R data frame (tibble)
```

*Note:* If a webpage has more than one table, simply apply the `html_elements()` function in place of `html_element()`, which will import each of the desired tables as a list. You can then access your desired table by entering the index corresponding to the order of tables on the web page from top down.

```r
 data_tbl <- read_html(my_url) %>%
  html_elements("table") %>% # get all table elements on webpage and combine them into a list
  html_table() %>%
  .[[1]] # get first table
```

For a more in-depth description of web-page characteristics and HTML, see the opening sections of the dataquest article linked here: [Tutorial: Web Scraping in R with rvest](https://www.dataquest.io/blog/web-scraping-in-r-rvest/)

### 4. Clean dataset header

Two major issues often arise when scraping sports reference web pages, as shown in the screenshots below:

**A** <br>
<img width="588" alt="image" src="https://user-images.githubusercontent.com/112500643/192927742-5b81ff1f-d8ad-4c17-874e-88db707d51f7.png">

![image](https://user-images.githubusercontent.com/112500643/192931190-9101dfca-8d8c-4432-a2f7-da0dbdae6ffe.png)


**B** <br>
<img width="589" alt="image" src="https://user-images.githubusercontent.com/112500643/192930202-b1e73ea4-55c6-4d83-819e-0fc74639739a.png">


**A**: R confuses an extra header line as the true column names, and stores the true column names as the first row in the dataset <br>
**B** Sports Reference pastes a reminder of the column names after every 20 rows in the dataset, which creates useless observations within the dataset <br>


These problems can be fixed in three simple lines of code:

1) Use the `paste0()` and `colnames()` functions to paste the current column names together with the current first row, and store this vector of names as the new table column names.
2) Use the `gsub()` and `colnames()` functions to find and replace any unecessary periods in the columns that did not have any informating in the extra header line (usually the first 5 columns).
3) Use the `grepl()` function in a slice of the data_tbl along with the `!` "except" wildcard to only select observations that do not include header information. This can be found by searching for observations with the occurence of a column name in a given column, such as finding "Rk" in the `Rk` column.

```r
# combine first row with second level of header above with period in between as new column names
colnames(data_tbl) = paste0(colnames(data_tbl), ".", data_tbl[1,]) # paste "original column name.value in first row" together as new column name

# remove periods from first few columns, which did not have a second, upper level heading
colnames(data_tbl)[1:5] = gsub("\\.", "", colnames(data_tbl[1:5]))  # find and replace all periods in first 5 columns with nothing (i.e., "")

# remove unneeded repeated header rows
data_tbl_clean = data_tbl[!grepl('Rk', data_tbl$Rk), ] # search for and do not include observations with "Rk" in the Rk column
```




### 5. Compile commands as single function for ease of use // Convert columns to correct data type to prepare for analysis

### Complete Code for Webscraping Sports Reference in R

```r

```


### *Bonus Step*: Store webscraping commands as a function for importing from multiple data sources at once 


... and bind them together using purrr library
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

 
