---
title: "Midterm 1 W24"
author: "Jocelyn Morales"
date: "2024-02-06"
output:
  html_document: 
    keep_md: yes
  pdf_document: default
---

## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your code must be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run. Be sure to add your name to the author header above. 

Your code must knit in order to be considered. If you are stuck and cannot answer a question, then comment out your code and knit the document. You may use your notes, labs, and homework to help you complete this exam. Do not use any other resources- including AI assistance.  

Don't forget to answer any questions that are asked in the prompt!  

Be sure to push your completed midterm to your repository. This exam is worth 30 points.  

## Background
In the data folder, you will find data related to a study on wolf mortality collected by the National Park Service. You should start by reading the `README_NPSwolfdata.pdf` file. This will provide an abstract of the study and an explanation of variables.  

The data are from: Cassidy, Kira et al. (2022). Gray wolf packs and human-caused wolf mortality. [Dryad](https://doi.org/10.5061/dryad.mkkwh713f). 

## Load the libraries

```r
library("tidyverse")
library("janitor")
```

## Load the wolves data
In these data, the authors used `NULL` to represent missing values. I am correcting this for you below and using `janitor` to clean the column names.

```r
wolves <- read.csv("data/NPS_wolfmortalitydata.csv", na = c("NULL")) %>% clean_names()
```

## Questions
Problem 1. (1 point) Let's start with some data exploration. What are the variable (column) names?  

```r
names(wolves)
```

```
##  [1] "park"         "biolyr"       "pack"         "packcode"     "packsize_aug"
##  [6] "mort_yn"      "mort_all"     "mort_lead"    "mort_nonlead" "reprody1"    
## [11] "persisty1"
```


Problem 2. (1 point) Use the function of your choice to summarize the data and get an idea of its structure.  

```r
glimpse(wolves)
```

```
## Rows: 864
## Columns: 11
## $ park         <chr> "DENA", "DENA", "DENA", "DENA", "DENA", "DENA", "DENA", "…
## $ biolyr       <int> 1996, 1991, 2017, 1996, 1992, 1994, 2007, 2007, 1995, 200…
## $ pack         <chr> "McKinley River1", "Birch Creek N", "Eagle Gorge", "East …
## $ packcode     <int> 89, 58, 71, 72, 74, 77, 101, 108, 109, 53, 63, 66, 70, 72…
## $ packsize_aug <dbl> 12, 5, 8, 13, 7, 6, 10, NA, 9, 8, 7, 11, 0, 19, 15, 12, 1…
## $ mort_yn      <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
## $ mort_all     <int> 4, 2, 2, 2, 2, 2, 2, 2, 2, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
## $ mort_lead    <int> 2, 2, 0, 0, 0, 0, 1, 2, 1, 1, 1, 0, 0, 0, 1, 1, 1, 0, 0, …
## $ mort_nonlead <int> 2, 0, 2, 2, 2, 2, 1, 0, 1, 0, 0, 1, 1, 1, 0, 0, 0, 1, 1, …
## $ reprody1     <int> 0, 0, NA, 1, NA, 0, 0, 1, 0, 1, 0, 1, 0, 1, 1, 1, 1, 1, 1…
## $ persisty1    <int> 0, 0, 1, 1, 1, 1, 0, 1, 0, 1, 0, 1, 0, 1, 1, 1, 1, 1, 1, …
```


Problem 3. (3 points) Which parks/ reserves are represented in the data? Don't just use the abstract, pull this information from the data.  

```r
wolves %>% 
  count(park)
```

```
##   park   n
## 1 DENA 340
## 2 GNTP  77
## 3  VNP  48
## 4  YNP 248
## 5 YUCH 151
```


Problem 4. (4 points) Which park has the largest number of wolf packs?

```r
wolves %>%
  group_by(park) %>% 
  count(packsize_aug, sort = T)
```

```
## # A tibble: 98 × 3
## # Groups:   park [5]
##    park  packsize_aug     n
##    <chr>        <dbl> <int>
##  1 VNP             NA    38
##  2 DENA             2    37
##  3 DENA             6    37
##  4 DENA             8    36
##  5 DENA             7    30
##  6 DENA             3    28
##  7 DENA             5    26
##  8 DENA            10    22
##  9 DENA             9    19
## 10 YUCH             2    19
## # ℹ 88 more rows
```


Problem 5. (4 points) Which park has the highest total number of human-caused mortalities `mort_all`?

```r
wolves %>% 
  group_by(park) %>% 
  count(mort_all)
```

```
## # A tibble: 28 × 3
## # Groups:   park [5]
##    park  mort_all     n
##    <chr>    <int> <int>
##  1 DENA         0   287
##  2 DENA         1    44
##  3 DENA         2     8
##  4 DENA         4     1
##  5 GNTP         0    53
##  6 GNTP         1    15
##  7 GNTP         2     6
##  8 GNTP         3     1
##  9 GNTP         4     2
## 10 VNP          0    39
## # ℹ 18 more rows
```


The wolves in [Yellowstone National Park](https://www.nps.gov/yell/learn/nature/wolf-restoration.htm) are an incredible conservation success story. Let's focus our attention on this park.  

Problem 6. (2 points) Create a new object "ynp" that only includes the data from Yellowstone National Park.  

```r
ynp <- wolves %>% 
  filter(park=="YNP")
```

Problem 7. (3 points) Among the Yellowstone wolf packs, the [Druid Peak Pack](https://www.pbs.org/wnet/nature/in-the-valley-of-the-wolves-the-druid-wolf-pack-story/209/) is one of most famous. What was the average pack size of this pack for the years represented in the data?

```r
ynp %>% 
  filter(pack=="druid") %>% 
  summarize(mean_pack_size=mean(packsize_aug))
```

```
##   mean_pack_size
## 1       13.93333
```

Problem 8. (4 points) Pack dynamics can be hard to predict- even for strong packs like the Druid Peak pack. At which year did the Druid Peak pack have the largest pack size? What do you think happened in 2010?

The year that the Druid Peak pack was at it's largest size was in the year 2001. In 2010, I think there may have been an infectious disease that may have spread through the pack, killing them all. 


```r
ynp %>% 
  filter(pack=="druid") %>% 
  count(pack, packsize_aug, biolyr) %>% 
  arrange(desc(packsize_aug))
```

```
##     pack packsize_aug biolyr n
## 1  druid           37   2001 1
## 2  druid           27   2000 1
## 3  druid           21   2008 1
## 4  druid           18   2003 1
## 5  druid           18   2007 1
## 6  druid           16   2002 1
## 7  druid           15   2006 1
## 8  druid           13   2004 1
## 9  druid           12   2009 1
## 10 druid            9   1999 1
## 11 druid            8   1998 1
## 12 druid            5   1996 1
## 13 druid            5   1997 1
## 14 druid            5   2005 1
## 15 druid            0   2010 1
```

Problem 9. (5 points) Among the YNP wolf packs, which one has had the highest overall persistence `persisty1` for the years represented in the data? Look this pack up online and tell me what is unique about its behavior- specifically, what prey animals does this pack specialize on?  


```r
ynp %>% 
  group_by(pack) %>% 
  count(pack, persisty1) %>% 
  arrange(desc(persisty1))
```

```
## # A tibble: 67 × 3
## # Groups:   pack [46]
##    pack        persisty1     n
##    <chr>           <int> <int>
##  1 682Mgroup           1     1
##  2 8mile               1     9
##  3 agate               1    10
##  4 bechler             1     2
##  5 biscuit             1     1
##  6 blacktail           1     5
##  7 buffalofork         1     1
##  8 canyon              1     9
##  9 cinnabar            1     1
## 10 cottonwood          1     1
## # ℹ 57 more rows
```


Problem 10. (3 points) Perform one analysis or exploration of your choice on the `wolves` data. Your answer needs to include at least two lines of code and not be a summary function.  

```r
wolves %>% 
  group_by(pack) %>% 
  summarize(mean_mort_all=mean(mort_all),
            total=n()) %>% 
  arrange(desc(mean_mort_all))
```

```
## # A tibble: 184 × 3
##    pack            mean_mort_all total
##    <chr>                   <dbl> <int>
##  1 Sheep Bluff              4        3
##  2 Webber Creek 2           4        1
##  3 Yukon Fork               3        4
##  4 Lost Creek               2.86     7
##  5 70 Mile                  2.46    13
##  6 642Fgroup                2        1
##  7 Birch Creek N            2        1
##  8 Fourth of July           2        1
##  9 cottonwood               2        2
## 10 Copper Mountain          1.75     4
## # ℹ 174 more rows
```

