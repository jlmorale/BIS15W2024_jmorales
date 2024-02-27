---
title: "Midterm 2 Material"
author: "Jocelyn Morales"
date: "2024-02-27"
output: 
  html_document: 
    keep_md: true
---



## Libraries 

```r
#tidyverse
#naniar
#janitor
```


## Lab 8 

```r
#find NA 
#1. data %>% 
#  map_df(~sum(is.na(.)))

#2. naniar::miss_var_summary(data)

#replace the NAs
#data %>% 
# replace_with_na(replace= list(newborn = "not measured)) %>% 
# miss_var_summary()
```

## Lab 9

```r
#make data "tidy" 
#data %>% 
#  pivot_longer(-variable,
#               names_to = "new variable",
#               names_sep = "_" #seperates the names into individual names 
#               values_to = "values")

#make data easier to read for other people 
#data %>% 
#  pivot_wider(-variable,
#              names_to = "new variable",
#              values_to = "values"))

#separate names into two different column names 
#data %>% 
#  separate(variable, into = c("variable1, variable2"), sep = "how are the variables separted")
```

## Lab 10 

```r
#scatterplot(two continous data)
#ggplot(aes(x=varaiable1,  y=variable2))+
#  geom_point() or geom_jitter()

#geom_bar(), variable that does not have continous data 
#ggplot(aes(x=variable))+
#  geom_bar()

#geom_col(), paired with continous data and non continous data 
#ggplot(aes(x=noncontinous, y= continous))+
#  geom_col()

#boxplots 
#ggplot(aes(x=noncontinous, y=continous))+
#  geom_boxplot()
```

## Lab 11

```r
#adding titles
#labs(title = "",
#     x= "",
#     y="")

#fixing the titles
#theme(plot.title = element_text (size = rel(1.5), #hjust = 0.5),
#      axis.text.x = element_text(angle=50, #hjust=1))

#remove NA in data plots 
#geom_col(na.rm = T) or filter(variable != "NA)

#flip chart 
#coord_flip()

#separate data 
#geom_bar(position = "dodge")

#add color
#ggplot(aes(x=variable, fill = variable2))
```

remeber we can combine the codes to have multiple visualez in one graph.
