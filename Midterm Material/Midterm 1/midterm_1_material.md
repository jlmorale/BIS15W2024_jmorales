---
title: "Midterm 1 Material"
author: "Jocelyn Morales"
date: "2024-02-06"
output: 
  html_document: 
    keep_md: true
---



## Useful Libraries to uplaod


```r
#library("tidyverse") 
#library("janitor")
#library("skimr")
```

## How to upload data? Use the "read.csv()" code


```r
#Example:
#object <- read.csv("data/name_of_file") # inside the quotes add the location of data and name of data
```

## Ways to look at the data


```r
#each give show practically the same thing but in different ways
#glimpse()
#summary()
#dim()
#str()
#skim()
#names() #shows the names of the columns
```

## With the help of the 'janitor' librabry we can clean up the data if needed


```r
#clean_names(data_frame_name) #this will clean up any uppercase and weirdly labeled variables in the data

#you can also use rename
#rename()
#example 
#rename(data_frame_name, name_on_data_frame = "new_name")
```

## Packages we have used: dplyr


```r
#filter() #will pull out the row names of interest 
#within filter you can use these:
#filter(condition1 & condition2) will return condition1 and condition2 are met.
#filter(condition1, condition2) will return rows where both conditions are met.
#filter(condition1, !condition2) will return all rows where condition one is true but condition 2 is not.
#filter(condition1 | condition2) will return rows where condition 1 or condition 2 is met.
#filter(xor(condition1, condition2) will return all rows where only one of the conditions is met, and not when both conditions are met.
#between()
#near()
#%in%=within 
#remember to use ==, <=, >=, != (not equal to)

#select() #will pull out the column names of interest
#within select you can use these: 
#ends_with() = Select columns that end with a character string  
#contains() = Select columns that contain a character string  
#matches() = Select columns that match a regular expression  
#one_of() = Select columns names that are from a group of names  
#adding a (-) can be used to excludes the specific variables not wanted
```

## Mean


```r
#mean()#this is the basic form
#example:
#mean(data_frame$variable)
#min()
#max()
#for both min and max it should be written in the same way as mean 
#to remove NAs use 'na.rm = T'
```

## Change data class to a different type


```r
#as.factor()
#as.character()
#as.integer()
#as.numeric()
#example:
#data_frame$variable <- as.factor(data_frame$variable)

#to look for the class type of a variable 
#class(data_frame$variable)
```

## Pipes


```r
#with pipes you can have one huge code to have a much more organized panel
#example: 
#fish %>% #work with the fish data
#  select(lakeid, radii_length_mm) %>% #pull out variable of interest
#  filter(lakeid=="AL" | lakeid=="AR") %>% #only these lakes
#  filter(between(radii_length_mm, 2,4)) %>% #between 2 and 4 
#  arrange(desc(radii_length_mm)) #sort to make easier to read the numbers will descending
```

## Mutate


```r
#Mutate allows us to create a new column from existing columns in a data frame:
#fish %>% 
#  mutate(length_mm = length*10) %>% 
#  select(fish_id, length, length_mm)

#changes all entries to lowercase (if present), for uppercase 'toupper': 
#mammals %>%
#  mutate_all(tolower) 

#mutate can also work in specific individual columns: 
#mammals %>% 
#  mutate(across(c("order", "family"), tolower))

#we can also specify with 'ifelse()':
#mammals %>% 
#  select(family, genus, species, max_life) %>% 
#  mutate(max_life_new = ifelse(max_life == -999.00, NA, max_life)) %>% #mutate all in max_life that has a value of -999.00 to an NA, otherwise leave as max_life value
#  arrange(desc(max_life_new))
```

## Summarize

```r
#many different variables can be used 
#example:
#msleep %>% 
#  filter(bodywt>200) %>% 
#  summarize(mean_sleep_lg=mean(sleep_total),
#            min_sleep_lg=min(sleep_total),
#            max_sleep_lg=max(sleep_total),
#            sd_sleep_lg=sd(sleep_total),
#            total=n()) #tells us the number of observations 

#look for a number of distinct observations: 
#msleep %>% 
#  summarize(n_genera=n_distinct(genus)) #this is going to count the number of genera in msleep

#group by: 
#msleep %>%
#  group_by(vore) %>% #we are grouping by feeding ecology, a categorical variable before doing the summary
#  summarize(min_bodywt = min(bodywt),
#            max_bodywt = max(bodywt),
#            mean_bodywt = mean(bodywt),
#            total=n())

#we can pull data not including the NAs:
#penguins %>% 
#  filter(!is.na(body_mass_g)) %>% #we are pulling out all of the observations that are numbers not the NAs
#  group_by(island) %>% 
#   summarize(mean_body_mass=mean(body_mass_g),
#            total=n())

#how do we find the number of penguins in each island, can with a single variable or multiple:
#penguins %>% 
#  count(island, species, sort = T) #sort=T sorts the column in descending order

#another option similar to count:
#penguins %>% 
#  tabyl(island, species)
```

