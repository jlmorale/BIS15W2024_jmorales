---
title: "lab3_warmup"
author: "jocelyn morales"
date: "2024-01-18"
output: 
  html_document: 
    keep_md: yes
---



### 1. Plant Height Vector 


```r
plant_height <- c(30.7, 37.6, 28.4, NA, 33.2)
```

### 2. Plant Mass Vector 


```r
plant_weight <- c(4, 5.2, 3.7, NA, 4.6)
```

### 3. Labels for data matrix 


```r
samples <- c("plant_1", "plant_2", "plant_3", "plant_4", "plant_5")
meaasured <- c("height", "weight")
```

### 4. Combine data for height and weight 


```r
plant_experiment <- c(plant_height, plant_weight)
```

### 5. Build the data matrix 


```r
plant_experiment_matrix <- matrix(plant_experiment, nrow = 5, byrow = F)
plant_experiment_matrix
```

```
##      [,1] [,2]
## [1,] 30.7  4.0
## [2,] 37.6  5.2
## [3,] 28.4  3.7
## [4,]   NA   NA
## [5,] 33.2  4.6
```
### 6. Name the columns and rows 


```r
colnames(plant_experiment_matrix) <- meaasured
rownames(plant_experiment_matrix) <- samples
plant_experiment_matrix
```

```
##         height weight
## plant_1   30.7    4.0
## plant_2   37.6    5.2
## plant_3   28.4    3.7
## plant_4     NA     NA
## plant_5   33.2    4.6
```

### 7. Calculate the means of each column 


```r
plant_means <- colMeans(plant_experiment_matrix, na.rm = T)
plant_means
```

```
## height weight 
## 32.475  4.375
```

### 8. Add this as a new row 


```r
plant_experiment_matrix_final <- rbind(plant_experiment_matrix, plant_means)
plant_experiment_matrix_final
```

```
##             height weight
## plant_1     30.700  4.000
## plant_2     37.600  5.200
## plant_3     28.400  3.700
## plant_4         NA     NA
## plant_5     33.200  4.600
## plant_means 32.475  4.375
```

