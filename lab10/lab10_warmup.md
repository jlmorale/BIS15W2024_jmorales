---
title: "lab10_warmup"
author: "Jocelyn Morales"
date: "2024-02-15"
output: 
  html_document: 
    keep_md: yes
---



## 1. In the data folder there is an epidemiology data set on an outbreak of malaria. 

```r
library(tidyverse)
```

```
## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
## ✔ dplyr     1.1.4     ✔ readr     2.1.4
## ✔ forcats   1.0.0     ✔ stringr   1.5.1
## ✔ ggplot2   3.4.4     ✔ tibble    3.2.1
## ✔ lubridate 1.9.3     ✔ tidyr     1.3.0
## ✔ purrr     1.0.2     
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```

```r
library(janitor)
```

```
## 
## Attaching package: 'janitor'
## 
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```


```r
malaria <- read_csv("data/malaria.csv") %>%  clean_names()
```

```
## Rows: 3038 Columns: 10
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (3): location_name, Province, District
## dbl  (5): malaria_rdt_0-4, malaria_rdt_5-14, malaria_rdt_15, malaria_tot, newid
## date (2): data_date, submitted_date
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```
## 2. rdt refers to rapid diasgnostic test and they are identified here by age group. 

```r
names(malaria)
```

```
##  [1] "location_name"    "data_date"        "submitted_date"   "province"        
##  [5] "district"         "malaria_rdt_0_4"  "malaria_rdt_5_14" "malaria_rdt_15"  
##  [9] "malaria_tot"      "newid"
```

## 3. Make the data tidy and store them as a new object 

```r
malaria_2 <- malaria %>% 
  pivot_longer(cols = starts_with("malaria_rdt"),
               names_to = "age_class",
               values_to = "cases") %>% 
  select(newid, data_date, submitted_date, location_name, province, district, age_class, cases)
```

## 4. Which district had the highest total number of cases on July 30, 2020

```r
malaria_2 %>% 
  filter(data_date=="2020-07-30") %>% 
  group_by(district) %>% 
  summarise(tot_cases= sum(cases, na.rm =T)) %>% 
  arrange(-tot_cases)
```

```
## # A tibble: 4 × 2
##   district tot_cases
##   <chr>        <dbl>
## 1 Bolo           347
## 2 Dingo          218
## 3 Spring         140
## 4 Barnard         77
```

