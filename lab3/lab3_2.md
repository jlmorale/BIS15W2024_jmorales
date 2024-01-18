---
title: "Importing Data Frames"
date: "2024-01-18"
output:
  html_document: 
    theme: spacelab
    toc: yes
    toc_float: yes
    keep_md: yes
  pdf_document:
    toc: yes
---

## Learning Goals
*At the end of this exercise, you will be able to:*    
1. Import .csv files as data frames using `read_csv()`.  
2. Use summary functions to explore the dimensions, structure, and contents of a data frame.  
3. Use the `select()` command of dplyr to sort data frames.  

## Review
At this point, you should have familiarity in RStudio, GitHub, and basic operations in R. You understand how to do arithmetic, assign values to objects, and work with vectors, data matrices, and data frames. If you are confused or need some extra help, please [email me](mailto: jmledford@ucdavis.edu).  

## Load the tidyverse

```r
library("tidyverse")
```

## Data Frames
For the remainder of the course, we will work exclusively with data frames. Recall that data frames store multiple classes of data. Last time, you were shown how to build data frames using the `data.frame()` command. However, scientists often make their data available as supplementary material associated with a publication. This is excellent scientific practice as it insures repeatability by showing exactly how analyses were performed. As data scientists, we capitalize on this by importing data directly into R.  

## Importing Data
R allows us to import a wide variety of data types. The most common type of file is a .csv file which stands for comma separated values. Spreadsheets are often developed in Excel then saved as .csv files for use in R. There are packages that allow you to open excel files and many other formats directly but .csv is the most common.  

An opinionated word about excel. It is fine to use excel for data entry and basic analysis. But, it often adds formatting that makes excel files difficult to work with in any program besides excel. R can read excel files, but I know of no R programmers that routinely use them. Instead they save copies of their excel files as .csv which strips away formatting but makes them easier to use in a variety of programs. We won't work with excel files in BIS 15L, but we will learn to import them.  

To import any file, first make sure that you are in the correct working directory. If you are not in the correct directory, R will not "see" the file.

```r
getwd()
```

```
## [1] "/Users/jlmorale/Desktop/BIS15W2024_jmorales/lab3"
```

## Load the data
Here we open a .csv file. Since we are using the tidyverse, we open the file using `read_csv()`. `readr` is included in the tidyverse set of packages. We specify the package and function with the `::` symbol. This becomes important if you have multiple packages loaded that contain functions with the same name.  

In the previous part of the lab, you exported a `.csv` of hot springs data. Let's try to reload that `.csv`.  

```r
hot_spring <- read_csv("hsprings_data.csv")
```

```
## Rows: 9 Columns: 4
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (2): scientist, spring
## dbl (2): temp_C, depth_ft
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

Use the `str()` function to get an idea of the data structure of `hot_springs`.  

```r
str(hot_spring)
```

```
## spc_tbl_ [9 × 4] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ temp_C   : num [1:9] 36.2 35.4 35.3 35.1 35.4 ...
##  $ scientist: chr [1:9] "Jill" "Susan" "Steve" "Jill" ...
##  $ spring   : chr [1:9] "Buckeye" "Buckeye" "Buckeye" "Benton" ...
##  $ depth_ft : num [1:9] 4.15 4.13 4.12 3.21 3.23 3.2 5.67 5.65 5.66
##  - attr(*, "spec")=
##   .. cols(
##   ..   temp_C = col_double(),
##   ..   scientist = col_character(),
##   ..   spring = col_character(),
##   ..   depth_ft = col_double()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

What is the class of the scientist column? Change it to factor and then show the levels of that factor.  

```r
class(hot_spring$scientist)
```

```
## [1] "character"
```


```r
hot_spring$scientist <- as.factor(hot_spring$scientist) #replace scientist in the hot spring data frame from a character to a factor 
hot_spring$spring <- as.factor(hot_spring$spring) # now try changing springs from character to factor
```


```r
levels(hot_spring$scientist) #a factor is a repeated category just like the names, tell us 
```

```
## [1] "Jill"  "Steve" "Susan"
```

```r
levels(hot_spring$spring) 
```

```
## [1] "Benton"     "Buckeye"    "Travertine"
```

## Practice
1. In your lab 3 folder there is another folder titled `data`. Inside the `data` folder there is a `.csv` titled `Gaeta_etal_CLC_data.csv`. Open this data and store them as an object called `fish`.  

The data are from: Gaeta J., G. Sass, S. Carpenter. 2012. Biocomplexity at North Temperate Lakes LTER: Coordinated Field Studies: Large Mouth Bass Growth 2006. Environmental Data Initiative.  [link](https://portal.edirepository.org/nis/mapbrowse?scope=knb-lter-ntl&identifier=267)  

```r
fish <- read_csv("data/Gaeta_etal_CLC_data.csv")
```

```
## Rows: 4033 Columns: 6
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (2): lakeid, annnumber
## dbl (4): fish_id, length, radii_length_mm, scalelength
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

2. What is the structure of these data?

```r
str(fish)
```

```
## spc_tbl_ [4,033 × 6] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ lakeid         : chr [1:4033] "AL" "AL" "AL" "AL" ...
##  $ fish_id        : num [1:4033] 299 299 299 300 300 300 300 301 301 301 ...
##  $ annnumber      : chr [1:4033] "EDGE" "2" "1" "EDGE" ...
##  $ length         : num [1:4033] 167 167 167 175 175 175 175 194 194 194 ...
##  $ radii_length_mm: num [1:4033] 2.7 2.04 1.31 3.02 2.67 ...
##  $ scalelength    : num [1:4033] 2.7 2.7 2.7 3.02 3.02 ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   lakeid = col_character(),
##   ..   fish_id = col_double(),
##   ..   annnumber = col_character(),
##   ..   length = col_double(),
##   ..   radii_length_mm = col_double(),
##   ..   scalelength = col_double()
##   .. )
##  - attr(*, "problems")=<externalptr>
```


```r
glimpse(fish)
```

```
## Rows: 4,033
## Columns: 6
## $ lakeid          <chr> "AL", "AL", "AL", "AL", "AL", "AL", "AL", "AL", "AL", …
## $ fish_id         <dbl> 299, 299, 299, 300, 300, 300, 300, 301, 301, 301, 301,…
## $ annnumber       <chr> "EDGE", "2", "1", "EDGE", "3", "2", "1", "EDGE", "3", …
## $ length          <dbl> 167, 167, 167, 175, 175, 175, 175, 194, 194, 194, 194,…
## $ radii_length_mm <dbl> 2.697443, 2.037518, 1.311795, 3.015477, 2.670733, 2.13…
## $ scalelength     <dbl> 2.697443, 2.697443, 2.697443, 3.015477, 3.015477, 3.01…
```

```r
names(fish)
```

```
## [1] "lakeid"          "fish_id"         "annnumber"       "length"         
## [5] "radii_length_mm" "scalelength"
```

Notice that when the data are imported, you are presented with a message that tells you how R interpreted the column classes. This is also where error messages will appear if there are problems.  

## Summary functions
Once data have been uploaded, you may want to get an idea of its structure, contents, and dimensions. I routinely run one or more of these commands when data are first imported.  

We can summarize our data frame with the`summary()` function.  

```r
summary(fish)
```

```
##     lakeid             fish_id       annnumber             length     
##  Length:4033        Min.   :  1.0   Length:4033        Min.   : 58.0  
##  Class :character   1st Qu.:156.0   Class :character   1st Qu.:253.0  
##  Mode  :character   Median :267.0   Mode  :character   Median :299.0  
##                     Mean   :258.3                      Mean   :293.3  
##                     3rd Qu.:376.0                      3rd Qu.:342.0  
##                     Max.   :478.0                      Max.   :420.0  
##  radii_length_mm    scalelength     
##  Min.   : 0.4569   Min.   : 0.6282  
##  1st Qu.: 2.3252   1st Qu.: 4.2596  
##  Median : 3.5380   Median : 5.4062  
##  Mean   : 3.6589   Mean   : 5.3821  
##  3rd Qu.: 4.8229   3rd Qu.: 6.4145  
##  Max.   :11.0258   Max.   :11.0258
```

`glimpse()` is another useful summary function.

```r
glimpse(fish)
```

```
## Rows: 4,033
## Columns: 6
## $ lakeid          <chr> "AL", "AL", "AL", "AL", "AL", "AL", "AL", "AL", "AL", …
## $ fish_id         <dbl> 299, 299, 299, 300, 300, 300, 300, 301, 301, 301, 301,…
## $ annnumber       <chr> "EDGE", "2", "1", "EDGE", "3", "2", "1", "EDGE", "3", …
## $ length          <dbl> 167, 167, 167, 175, 175, 175, 175, 194, 194, 194, 194,…
## $ radii_length_mm <dbl> 2.697443, 2.037518, 1.311795, 3.015477, 2.670733, 2.13…
## $ scalelength     <dbl> 2.697443, 2.697443, 2.697443, 3.015477, 3.015477, 3.01…
```

`nrow()` gives the numbers of rows.

```r
nrow(fish)
```

```
## [1] 4033
```

`ncol` gives the number of columns.

```r
ncol(fish)
```

```
## [1] 6
```

`dim()` gives the dimensions.

```r
dim(fish)
```

```
## [1] 4033    6
```

`names` gives the column names.

```r
names(fish)
```

```
## [1] "lakeid"          "fish_id"         "annnumber"       "length"         
## [5] "radii_length_mm" "scalelength"
```

`head()` prints the first n rows of the data frame.

```r
head(fish)
```

```
## # A tibble: 6 × 6
##   lakeid fish_id annnumber length radii_length_mm scalelength
##   <chr>    <dbl> <chr>      <dbl>           <dbl>       <dbl>
## 1 AL         299 EDGE         167            2.70        2.70
## 2 AL         299 2            167            2.04        2.70
## 3 AL         299 1            167            1.31        2.70
## 4 AL         300 EDGE         175            3.02        3.02
## 5 AL         300 3            175            2.67        3.02
## 6 AL         300 2            175            2.14        3.02
```

`tail()` prinst the last n rows of the data frame.

```r
tail(fish)
```

```
## # A tibble: 6 × 6
##   lakeid fish_id annnumber length radii_length_mm scalelength
##   <chr>    <dbl> <chr>      <dbl>           <dbl>       <dbl>
## 1 WS         180 6            403            5.41        11.0
## 2 WS         180 5            403            4.98        11.0
## 3 WS         180 4            403            4.22        11.0
## 4 WS         180 3            403            3.04        11.0
## 5 WS         180 2            403            2.03        11.0
## 6 WS         180 1            403            1.19        11.0
```

`table()` is useful when you have a limited number of categorical variables. It produces fast counts of the number of observations in a variable. We will come back to this later... 

```r
table(fish$lakeid)
```

```
## 
##  AL  AR  BO  BR  CR  DY  FD  JN  LC  LJ  LR LSG  MN  RD  UB  WS 
## 383 262 197 291 343 355 302 238 173 181 292 143 293 135 191 254
```

We can also click on the `fish` data frame in the Environment tab or type View(fish).

```r
#View(fish)
view(fish)
```

## Filter
Filter is a way of pulling out observations that meet specific criteria in a variable. We will work a lot more with this in the next lab.  

```r
little_fish <- filter(fish, length<=100)
little_fish
```

```
## # A tibble: 5 × 6
##   lakeid fish_id annnumber length radii_length_mm scalelength
##   <chr>    <dbl> <chr>      <dbl>           <dbl>       <dbl>
## 1 LSG         58 EDGE          92           1.15        1.15 
## 2 LSG         59 EDGE          64           0.773       0.773
## 3 WS         151 EDGE          58           0.628       0.628
## 4 WS         152 EDGE          74           0.832       0.832
## 5 WS         153 EDGE          78           0.637       0.637
```

## Practice
1. Load the data `mammal_lifehistories_v2.csv` and place it into a new object called `mammals`.

```r
mammals <- read_csv("data/mammal_lifehistories_v2.csv")
```

```
## Rows: 1440 Columns: 13
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (4): order, family, Genus, species
## dbl (9): mass, gestation, newborn, weaning, wean mass, AFR, max. life, litte...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

2. Provide the dimensions of the data frame.

```r
dim(mammals)
```

```
## [1] 1440   13
```

3. Check the column names in the data frame. 

```r
names(mammals)
```

```
##  [1] "order"        "family"       "Genus"        "species"      "mass"        
##  [6] "gestation"    "newborn"      "weaning"      "wean mass"    "AFR"         
## [11] "max. life"    "litter size"  "litters/year"
```

4. Use `str()` to show the structure of the data frame and its individual columns; compare this to `glimpse()`. 

```r
str(mammals)
```

```
## spc_tbl_ [1,440 × 13] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ order       : chr [1:1440] "Artiodactyla" "Artiodactyla" "Artiodactyla" "Artiodactyla" ...
##  $ family      : chr [1:1440] "Antilocapridae" "Bovidae" "Bovidae" "Bovidae" ...
##  $ Genus       : chr [1:1440] "Antilocapra" "Addax" "Aepyceros" "Alcelaphus" ...
##  $ species     : chr [1:1440] "americana" "nasomaculatus" "melampus" "buselaphus" ...
##  $ mass        : num [1:1440] 45375 182375 41480 150000 28500 ...
##  $ gestation   : num [1:1440] 8.13 9.39 6.35 7.9 6.8 5.08 5.72 5.5 8.93 9.14 ...
##  $ newborn     : num [1:1440] 3246 5480 5093 10167 -999 ...
##  $ weaning     : num [1:1440] 3 6.5 5.63 6.5 -999 ...
##  $ wean mass   : num [1:1440] 8900 -999 15900 -999 -999 ...
##  $ AFR         : num [1:1440] 13.5 27.3 16.7 23 -999 ...
##  $ max. life   : num [1:1440] 142 308 213 240 -999 251 228 255 300 324 ...
##  $ litter size : num [1:1440] 1.85 1 1 1 1 1.37 1 1 1 1 ...
##  $ litters/year: num [1:1440] 1 0.99 0.95 -999 -999 2 -999 1.89 1 1 ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   order = col_character(),
##   ..   family = col_character(),
##   ..   Genus = col_character(),
##   ..   species = col_character(),
##   ..   mass = col_double(),
##   ..   gestation = col_double(),
##   ..   newborn = col_double(),
##   ..   weaning = col_double(),
##   ..   `wean mass` = col_double(),
##   ..   AFR = col_double(),
##   ..   `max. life` = col_double(),
##   ..   `litter size` = col_double(),
##   ..   `litters/year` = col_double()
##   .. )
##  - attr(*, "problems")=<externalptr>
```


```r
glimpse(mammals)
```

```
## Rows: 1,440
## Columns: 13
## $ order          <chr> "Artiodactyla", "Artiodactyla", "Artiodactyla", "Artiod…
## $ family         <chr> "Antilocapridae", "Bovidae", "Bovidae", "Bovidae", "Bov…
## $ Genus          <chr> "Antilocapra", "Addax", "Aepyceros", "Alcelaphus", "Amm…
## $ species        <chr> "americana", "nasomaculatus", "melampus", "buselaphus",…
## $ mass           <dbl> 45375.0, 182375.0, 41480.0, 150000.0, 28500.0, 55500.0,…
## $ gestation      <dbl> 8.13, 9.39, 6.35, 7.90, 6.80, 5.08, 5.72, 5.50, 8.93, 9…
## $ newborn        <dbl> 3246.36, 5480.00, 5093.00, 10166.67, -999.00, 3810.00, …
## $ weaning        <dbl> 3.00, 6.50, 5.63, 6.50, -999.00, 4.00, 4.04, 2.13, 10.7…
## $ `wean mass`    <dbl> 8900, -999, 15900, -999, -999, -999, -999, -999, 157500…
## $ AFR            <dbl> 13.53, 27.27, 16.66, 23.02, -999.00, 14.89, 10.23, 20.1…
## $ `max. life`    <dbl> 142, 308, 213, 240, -999, 251, 228, 255, 300, 324, 300,…
## $ `litter size`  <dbl> 1.85, 1.00, 1.00, 1.00, 1.00, 1.37, 1.00, 1.00, 1.00, 1…
## $ `litters/year` <dbl> 1.00, 0.99, 0.95, -999.00, -999.00, 2.00, -999.00, 1.89…
```

5. . Try the `table()` command to produce counts of mammal order, family, and genus.  

```r
table(mammals$order)
```

```
## 
##   Artiodactyla      Carnivora        Cetacea     Dermoptera     Hyracoidea 
##            161            197             55              2              4 
##    Insectivora     Lagomorpha  Macroscelidea Perissodactyla      Pholidota 
##             91             42             10             15              7 
##       Primates    Proboscidea       Rodentia     Scandentia        Sirenia 
##            156              2            665              7              5 
##  Tubulidentata      Xenarthra 
##              1             20
```


```r
table(mammals$family)
```

```
## 
##     Abrocomidae       Agoutidae    Anomaluridae  Antilocapridae    Aplodontidae 
##               2               1               4               1               1 
##      Balaenidae Balaenopteridae    Bathyergidae         Bovidae    Bradypodidae 
##               3               6               8             103               3 
##  Callitrichidae       Camelidae         Canidae     Capromyidae      Castoridae 
##              18               6              31               6               2 
##        Caviidae         Cebidae Cercopithecidae        Cervidae  Cheirogaleidae 
##               9              27              58              30               6 
##   Chinchillidae Chrysochloridae Ctenodactylidae     Ctenomyidae  Cynocephalidae 
##               5               5               3               5               2 
##     Dasypodidae   Dasyproctidae  Daubentoniidae     Delphinidae      Dinomyidae 
##              12               4               1              23               1 
##       Dipodidae      Dugongidae      Echimyidae    Elephantidae         Equidae 
##              19               2               8               2               6 
##  Erethizontidae     Erinaceidae  Eschrichtiidae         Felidae     Galagonidae 
##               4              11               1              31               8 
##       Geomyidae      Giraffidae     Herpestidae    Heteromyidae  Hippopotamidae 
##              14               2              17              38               2 
##       Hominidae       Hyaenidae  Hydrochaeridae     Hylobatidae     Hystricidae 
##               4               4               1               7               7 
##        Indridae       Lemuridae       Leporidae         Loridae Macroscelididae 
##               5               9              31               5              10 
##         Manidae   Megaladapidae  Megalonychidae    Monodontidae       Moschidae 
##               7               3               2               2               3 
##         Muridae      Mustelidae   Myocastoridae        Myoxidae Myrmecophagidae 
##             376              46               1               9               3 
##   Neobalaenidae     Ochotonidae    Octodontidae      Odobenidae Orycteropodidae 
##               1              11               3               1               1 
##       Otariidae       Pedetidae    Petromuridae        Phocidae     Phocoenidae 
##              12               1               1              18               4 
##    Physeteridae   Platanistidae     Procaviidae     Procyonidae  Rhinocerotidae 
##               3               5               4               8               5 
##       Sciuridae  Solenodontidae       Soricidae          Suidae        Talpidae 
##             130               2              51               7              12 
##       Tapiridae       Tarsiidae     Tayassuidae      Tenrecidae   Thryonomyidae 
##               4               5               3              10               2 
##      Tragulidae    Trichechidae       Tupaiidae         Ursidae      Viverridae 
##               4               3               7               9              20 
##       Ziphiidae 
##               7
```


```r
table(mammals$Genus)
```

```
## 
##         Abrocoma         Acinonyx           Acomys            Addax 
##                2                1                4                1 
##        Aepyceros         Aethomys           Agouti       Ailuropoda 
##                1                4                1                1 
##          Ailurus           Akodon       Alcelaphus            Alces 
##                1                9                1                1 
##        Allactaga   Allenopithecus   Allocricetulus           Alopex 
##                4                1                1                1 
##         Alouatta         Alticola         Amblonyx       Amblysomus 
##                4                3                1                1 
##       Ammodorcas Ammospermophilus       Ammotragus       Anomalurus 
##                1                4                1                3 
##       Antidorcas      Antilocapra         Antilope            Aonyx 
##                1                1                1                2 
##            Aotus       Aplodontia         Apodemus        Arborimus 
##                3                1                7                3 
##        Arctictis       Arctocebus    Arctocephalus     Arctogalidia 
##                1                1                6                1 
##         Arctonyx      Arvicanthis         Arvicola         Atelerix 
##                1                1                2                3 
##           Ateles       Atelocynus        Atherurus           Atilax 
##                4                1                2                1 
##       Auliscomys            Avahi             Axis        Babyrousa 
##                1                1                2                1 
##          Baiomys          Balaena     Balaenoptera        Bandicota 
##                1                1                5                2 
##      Bassaricyon      Bassariscus       Bathyergus         Bdeogale 
##                1                2                2                1 
##           Beamys        Berardius            Bison          Blarina 
##                1                2                2                3 
##      Blastocerus          Bolomys              Bos       Boselaphus 
##                1                1                3                1 
##      Brachylagus      Brachyteles         Bradypus          Bubalus 
##                1                1                3                3 
##         Budorcas        Bunolagus        Cabassous          Cacajao 
##                1                1                1                1 
##       Callicebus        Callimico       Callithrix      Callorhinus 
##                3                1                6                1 
##     Callosciurus          Calomys       Calomyscus          Camelus 
##                4                5                2                2 
##            Canis         Cannomys          Caperea            Capra 
##                7                1                1                5 
##        Capreolus       Caprolagus         Capromys          Caracal 
##                2                1                1                1 
##           Castor        Catagonus         Catopuma            Cavia 
##                2                1                1                3 
##            Cebus      Cephalophus  Cephalorhynchus    Ceratotherium 
##                4               11                3                1 
##       Cercocebus    Cercopithecus        Cerdocyon           Cervus 
##                2               13                1                7 
##      Chaetodipus   Chaetophractus     Cheirogaleus       Chinchilla 
##                7                2                2                2 
##        Chionomys     Chiropodomys       Chiropotes       Chiruromys 
##                2                1                2                1 
##      Chlorocebus        Choloepus       Chrotogale    Chrysochloris 
##                1                2                1                2 
##       Chrysocyon     Chrysospalax      Civettictis    Clethrionomys 
##                1                1                1                5 
##          Coendou          Colobus          Colomys        Condylura 
##                1                4                1                1 
##        Conepatus        Conilurus     Connochaetes        Cremnomys 
##                3                1                2                2 
##       Cricetomys       Cricetulus         Cricetus        Crocidura 
##                1                2                1               13 
##          Crocuta      Crossarchus        Cryptomys     Cryptoprocta 
##                1                1                3                1 
##        Cryptotis    Ctenodactylus         Ctenomys             Cuon 
##                1                2                5                1 
##         Cyclopes         Cynictis     Cynocephalus         Cynogale 
##                1                1                2                1 
##          Cynomys       Cystophora             Dama       Damaliscus 
##                5                1                1                3 
##          Dasymys       Dasyprocta          Dasypus      Daubentonia 
##                1                3                5                1 
##   Delphinapterus        Delphinus      Dendrohyrax        Dendromus 
##                1                1                2                5 
##         Dephomys          Desmana   Desmodilliscus      Desmodillus 
##                1                1                1                1 
##     Dicerorhinus          Diceros      Dicrostonyx        Dinaromys 
##                1                1                5                1 
##          Dinomys     Diplomesodon        Dipodomys            Dipus 
##                1                1               14                1 
##       Dolichotis         Dremomys          Dryomys           Dugong 
##                2                1                2                1 
##          Echimys         Echinops      Echinosorex             Eira 
##                1                1                1                1 
##        Elaphodus        Elaphurus     Elephantulus          Elephas 
##                1                1                7                1 
##     Eligmodontia          Eliomys         Ellobius          Enhydra 
##                1                1                2                1 
##        Eolagurus         Epixerus            Equus       Eremitalpa 
##                1                1                6                1 
##       Eremodipus        Erethizon       Erignathus        Erinaceus 
##                1                1                1                2 
##     Erythrocebus     Eschrichtius        Eubalaena          Eulemur 
##                1                1                2                5 
##       Eumetopias         Euoticus       Euphractus         Eupleres 
##                1                1                1                1 
##     Exilisciurus            Felis           Feresa            Fossa 
##                1                4                1                1 
##       Funambulus      Funisciurus           Galago       Galagoides 
##                3                4                3                2 
##            Galea          Galemys        Galerella         Galictis 
##                2                1                2                1 
##          Galidia       Galidictis          Gazella          Genetta 
##                1                1               11                3 
##      Geocapromys          Geogale           Geomys        Georychus 
##                2                1                4                1 
##      Gerbillurus        Gerbillus          Giraffa        Glaucomys 
##                3               10                1                2 
##         Glirulus     Globicephala          Golunda          Gorilla 
##                1                2                1                1 
##        Grammomys          Grampus          Graomys       Graphiurus 
##                3                1                1                3 
##             Gulo      Halichoerus        Hapalemur        Helarctos 
##                1                1                2                1 
##     Heliophobius     Heliosciurus         Helogale     Hemicentetes 
##                1                1                1                1 
##      Hemiechinus        Hemigalus       Hemitragus      Herpailurus 
##                4                1                2                1 
##        Herpestes   Heterocephalus      Heterohyrax        Heteromys 
##                3                1                1                4 
##     Hexaprotodon     Hippocamelus     Hippopotamus      Hippotragus 
##                1                2                1                2 
##          Hodomys       Holochilus         Hoplomys           Hyaena 
##                1                1                1                1 
##          Hybomys     Hydrochaeris     Hydrodamalis         Hydromys 
##                1                1                1                1 
##       Hydropotes         Hydrurga       Hyemoschus        Hylobates 
##                1                1                1                7 
##      Hylochoerus          Hylomys       Hylomyscus        Hylopetes 
##                1                1                2                2 
##           Hyomys      Hyperacrius       Hyperoodon       Hypogeomys 
##                1                2                1                1 
##          Hystrix        Ichneumia          Ictonyx          Idiurus 
##                5                1                2                1 
##            Indri             Inia            Iomys          Jaculus 
##                1                1                1                3 
##    Kannabateomys          Kerodon            Kobus            Kogia 
##                1                1                5                2 
##    Lagenodelphis   Lagenorhynchus         Lagidium       Lagostomus 
##                1                4                2                1 
##        Lagothrix          Lagurus             Lama     Lasiopodomys 
##                1                1                3                1 
##        Leggadina        Lemmiscus           Lemmus      Lemniscomys 
##                2                1                2                2 
##            Lemur   Leontopithecus        Leopardus        Lepilemur 
##                1                1                3                3 
##       Leporillus      Leptailurus    Leptonychotes            Lepus 
##                1                1                1               14 
##        Limnogale           Liomys          Lipotes      Litocranius 
##                1                4                1                1 
##          Lobodon           Lontra        Lophiomys       Lophocebus 
##                1                3                1                1 
##       Lophuromys            Loris        Loxodonta            Lutra 
##                4                1                1                2 
##        Lutrogale           Lycaon             Lynx           Macaca 
##                1                1                4               13 
##    Macroscelides    Macrotarsomys          Madoqua         Makalata 
##                1                1                3                1 
##      Malacothrix       Mandrillus            Manis          Marmota 
##                1                2                7               13 
##           Martes      Massoutiera         Mastomys           Mazama 
##                6                1                2                3 
##     Megadontomys        Megaptera            Meles        Mellivora 
##                1                1                1                1 
##         Melogale          Melomys         Melursus         Mephitis 
##                1                8                1                2 
##         Meriones     Mesembriomys     Mesocricetus       Mesoplodon 
##               10                2                3                3 
##       Microcavia       Microcebus    Microdipodops        Microgale 
##                1                3                2                2 
##         Micromys  Micropotamogale         Microtus        Millardia 
##                1                1               29                1 
##      Miopithecus         Mirounga         Monachus          Monodon 
##                1                2                2                1 
##        Moschiola          Moschus           Mungos      Mungotictis 
##                1                3                1                1 
##        Muntiacus              Mus      Muscardinus          Mustela 
##                2               10                1               10 
##        Myocastor           Myomys        Myoprocta           Myopus 
##                1                3                1                1 
##       Myosciurus         Myosorex        Myospalax           Myoxus 
##                1                3                1                1 
##     Myrmecophaga        Mysateles        Mystromys      Naemorhedus 
##                1                2                1                3 
##         Nandinia      Nannospalax      Napaeozapus          Nasalis 
##                1                1                1                1 
##            Nasua         Neacomys         Nectomys         Neofelis 
##                2                1                2                1 
##         Neofiber           Neomys         Neophoca      Neophocaena 
##                1                2                1                1 
##          Neotoma       Neotomodon        Neotragus          Nesokia 
##               10                1                2                1 
##     Neurotrichus       Niviventer       Notiosorex          Notomys 
##                1                1                1                5 
##      Nyctereutes       Nycticebus         Nyctomys         Ochotona 
##                1                2                1               11 
##       Ochrotomys          Octodon     Octodontomys         Odobenus 
##                1                1                1                1 
##       Odocoileus          Oecomys          Oenomys           Okapia 
##                2                1                1                1 
##     Oligoryzomys      Ommatophoca        Oncifelis          Ondatra 
##                3                1                2                1 
##        Onychomys         Orcaella          Orcinus         Oreamnos 
##                2                1                1                1 
##       Oreotragus      Orthogeomys      Orycteropus      Oryctolagus 
##                1                2                1                1 
##             Oryx         Oryzomys           Otaria       Otocolobus 
##                3                3                1                1 
##          Otocyon         Otolemur           Otomys       Ototylomys 
##                1                2                5                1 
##          Ourebia           Ovibos             Ovis      Oxymycterus 
##                1                1                6                1 
##       Ozotoceros      Pachyuromys           Paguma              Pan 
##                1                1                1                2 
##         Panthera       Pantholops            Papio      Pappogeomys 
##                4                1                1                1 
##     Paracynictis      Paradoxurus       Parahyaena      Parascalops 
##                1                2                1                1 
##        Paraxerus       Pardofelis        Parotomys           Pecari 
##                5                1                1                1 
##          Pedetes            Pelea          Pelomys    Peponocephala 
##                1                1                2                1 
##     Perodicticus      Perognathus       Peromyscus       Petaurista 
##                1                7               24                5 
##        Petinomys      Petrodromus         Petromus      Petromyscus 
##                4                1                1                1 
##     Phacochoerus           Phaner       Phenacomys            Phoca 
##                1                1                2                7 
##       Phocarctos         Phocoena     Phocoenoides         Phodopus 
##                1                2                1                3 
##        Phyllotis         Physeter       Pithecheir         Pithecia 
##                1                1                1                2 
##     Plagiodontia       Platanista          Podomys      Poecilogale 
##                1                2                1                1 
##         Poelagus    Pogonomelomys        Pogonomys            Pongo 
##                1                1                3                1 
##       Pontoporia    Potamochoerus       Potamogale            Potos 
##                1                1                1                1 
##          Praomys        Presbytis       Priodontes     Prionailurus 
##                4                4                1                3 
##        Prionodon         Procapra         Procavia       Procolobus 
##                2                1                1                2 
##          Procyon       Proechimys         Profelis       Pronolagus 
##                2                3                1                3 
##      Propithecus         Proteles        Psammomys      Pseudalopex 
##                3                1                1                3 
##         Pseudois        Pseudomys        Pseudorca         Pteromys 
##                1               17                1                1 
##        Pteronura      Ptilocercus             Pudu             Puma 
##                1                1                2                1 
##        Pygathrix       Pygeretmus         Rangifer       Raphicerus 
##                2                2                1                1 
##           Rattus           Ratufa          Redunca       Reithrodon 
##               14                3                3                1 
##  Reithrodontomys        Rhabdomys       Rhinoceros     Rhinosciurus 
##                5                1                2                1 
##       Rhipidomys         Rhizomys        Rhombomys      Rhynchocyon 
##                2                2                1                1 
##      Romerolagus        Rupicapra      Saccostomus         Saguinus 
##                1                1                1               10 
##            Saiga          Saimiri      Salpingotus         Scalopus 
##                1                2                1                1 
##         Scapanus       Sciurillus          Sciurus       Scotinomys 
##                3                1               10                2 
##       Sekeetamys    Semnopithecus          Setifer          Sicista 
##                1                1                1                2 
##       Sigmoceros         Sigmodon        Solenodon            Sorex 
##                1                5                2               21 
##          Sotalia       Spalacopus           Spalax         Speothos 
##                1                1                1                1 
##  Spermophilopsis     Spermophilus       Sphiggurus        Spilogale 
##                1               31                2                2 
##        Steatomys         Stenella            Steno        Stochomys 
##                2                3                1                1 
##       Stylodipus           Suncus         Sundamys     Sundasciurus 
##                1                3                1                2 
##       Surdisorex         Suricata              Sus       Sylvicapra 
##                2                1                3                1 
##       Sylvilagus       Sylvisorex       Synaptomys         Syncerus 
##                8                1                2                1 
##     Tachyoryctes            Talpa         Tamandua           Tamias 
##                2                2                1               18 
##     Tamiasciurus          Tapirus          Tarsius         Tateomys 
##                2                4                5                1 
##           Tatera       Taterillus      Taurotragus          Taxidea 
##                8                3                2                1 
##          Tayassu           Tenrec       Tetracerus        Thallomys 
##                1                1                1                1 
##        Thamnomys    Theropithecus         Thomomys       Thrichomys 
##                1                1                7                1 
##       Thryonomys       Tolypeutes   Trachypithecus      Tragelaphus 
##                2                1                7                7 
##         Tragulus       Tremarctos       Trichechus      Trogopterus 
##                2                1                3                1 
##           Tupaia         Tursiops          Tylomys            Uncia 
##                5                1                1                1 
##         Uranomys          Urocyon          Urogale           Uromys 
##                1                2                1                1 
##       Urotrichus            Ursus      Vandeleuria          Varecia 
##                1                4                1                1 
##          Vicugna          Viverra      Viverricula          Vormela 
##                1                1                1                1 
##           Vulpes         Wiedomys            Xerus          Zaedyus 
##               10                1                2                1 
##         Zalophus            Zapus        Zelotomys          Ziphius 
##                1                3                1                1 
##     Zygodontomys          Zyzomys 
##                1                3
```


```r
table(mammals$species)
```

```
## 
##       abbreviatus            aberti           acouchy     acutorostrata 
##                 1                 1                 1                 1 
##            acutus         adspersus           adustus            aedium 
##                 1                 1                 1                 1 
##       aethiopicus          aethiops              afer              afra 
##                 2                 1                 1                 1 
##  africaeaustralis          africana         africanus            agilis 
##                 1                 1                 1                 2 
##          agrarius          agrestis         albicauda      albicaudatus 
##                 1                 1                 1                 1 
##         albifrons          albigena          albigula         albinasus 
##                 1                 1                 1                 1 
##         albinucha           albipes       albirostris       albiventris 
##                 1                 1                 2                 1 
##      albocinereus         alboniger             alces            alexis 
##                 1                 1                 1                 1 
##           algirus            alleni            alpina           alpinus 
##                 1                 6                 1                 1 
##           alstoni           altaica         amblyonyx         americana 
##                 2                 2                 1                 3 
##        americanus             ammon           amoenus         amphibius 
##                 3                 1                 1                 1 
##        ampullatus         andersoni        anerythrus           angasii 
##                 1                 1                 1                 1 
##        angolensis       angoniensis    angustirostris          anomalus 
##                 1                 1                 1                 2 
##          antimena        antisensis            apella            aperea 
##                 1                 1                 1                 1 
##        apereoides       apodemoides         aquaticus            aquilo 
##                 1                 1                 3                 1 
##       arachnoides           araneus          arboreus          arcticus 
##                 1                 1                 1                 2 
##         arctoides            arctos         arenarius         argentata 
##                 1                 1                 1                 1 
##        argentatus  argenteocinereus         argenteus     argentiventer 
##                 1                 1                 1                 1 
##           argurus             aries       arizonensis            armata 
##                 1                 1                 1                 1 
##           armatus           arnuxii         arundinum           arvalis 
##                 1                 1                 1                 1 
##          ascanius          asiatica            asinus           astutus 
##                 1                 1                 1                 1 
##         attenuata         attwateri         audubonii            aurata 
##                 2                 1                 1                 1 
##           auratus       aureogaster            aureus       auricularis 
##                 1                 1                 2                 1 
##            aurita           auritus         australis      avellanarius 
##                 1                 2                 4                 1 
##              axis            azarae            azarai         babyrussa 
##                 1                 1                 1                 1 
##          bachmani        bactrianus            badius         baibacina 
##                 1                 1                 2                 1 
##         bailwardi           bairdii          bancanus        barabensis 
##                 1                 3                 1                 1 
##           barbara          barbatus          bastardi            batesi 
##                 1                 2                 1                 1 
##          beecheyi         beecrofti         belangeri          beldingi 
##                 1                 1                 1                 1 
##         belzebuth          bendirii       bengalensis          bennetti 
##                 1                 1                 3                 1 
##         bennettii       berezovskii          betulina       bezoarticus 
##                 1                 1                 1                 1 
##           bicolor          bicornis            bidens             bieti 
##                 2                 1                 1                 1 
##          binotata         binturong             bison          bisulcus 
##                 1                 1                 1                 1 
##       blainvillei         blanfordi             bobak         bogdanovi 
##                 1                 1                 1                 1 
##       boliviensis           bonasus           booduga          borealis 
##                 1                 1                 1                 2 
##            bottae            boylii    brachyrhynchus         brachyura 
##                 1                 1                 1                 1 
##        brachyurus           brandti          brandtii         branickii 
##                 1                 1                 1                 1 
##          brantsii      brasiliensis           braueri       bredanensis 
##                 2                 3                 1                 1 
##        brevicauda      brevicaudata         breviceps      brevirostris 
##                 2                 1                 1                 1 
##           breweri           broweri           brownii            brucei 
##                 2                 1                 1                 1 
##           brunnea          brunneus           bubalis        bulbivorus 
##                 1                 1                 1                 1 
##        burchellii         bursarius           burtoni        buselaphus 
##                 1                 1                 1                 1 
##           buxtoni           byronia             cafer            caffer 
##                 1                 1                 1                 1 
##         cahirinus      calabarensis     californianus      californicus 
##                 1                 1                 1                 6 
##          caligata          callosus          callotis           calurus 
##                 1                 1                 1                 1 
##            calvus    camelopardalis         campbelli        campestris 
##                 1                 1                 2                 2 
##      camtschatica              cana        canadensis       canariensis 
##                 1                 1                 4                 1 
##       cancrivorus        canicaudus          caniceps           canipes 
##                 1                 1                 1                 1 
##             canus          capensis            capito         capreolus 
##                 1                 7                 1                 2 
##         capucinus           caracal            caraya     carcinophagus 
##                 1                 1                 1                 1 
##        carlhubbsi            caroli      carolinensis           caspica 
##                 1                 1                 2                 1 
##         castanops           catodon             catta         caucasica 
##                 1                 1                 1                 1 
##           caudata    caudimaculatus       cavirostris       cayennensis 
##                 1                 1                 1                 1 
##         centralis            cepapi       cephalophus            cephus 
##                 1                 1                 1                 1 
##        cervicapra        cervicolor        cervinipes          cervinus 
##                 1                 1                 1                 1 
##             chama             chaus         cheesmani          cherriei 
##                 1                 1                 1                 1 
##     chrotorrhinus      chrysogaster      chrysophilus       chrysopygus 
##                 1                 2                 1                 1 
##         chrysurus           cinerea     cinereicollis  cinereoargenteus 
##                 1                 3                 1                 1 
##          cinereus          citellus           civetta           clarkei 
##                 2                 1                 1                 1 
##           clusius      coeruleoalba          collaris          colletti 
##                 1                 1                 2                 1 
##          collinus          colocolo       columbianus            comata 
##                 1                 1                 1                 1 
##           cometes       commersonii          concolor          conditor 
##                 1                 1                 4                 1 
##          congicus           cooperi         coquereli         coronatus 
##                 2                 1                 1                 2 
##            corsac           coucang            coypus       crassicauda 
##                 1                 1                 1                 2 
##     crassicaudata    crassicaudatus        crassidens           crassus 
##                 1                 3                 1                 1 
##         crawfordi          cricetus          crinitus           crispus 
##                 1                 1                 1                 1 
##          cristata         cristatus           crocuta           crossei 
##                 4                 2                 1                 1 
##           cubanus          culpaeus         cuniculus           cupreus 
##                 1                 1                 1                 1 
##            cursor          curtatus         curzoniae         cutchicus 
##                 1                 1                 1                 1 
##           cuvieri            cyanus          cyclopis    cylindricornis 
##                 1                 1                 1                 1 
##             dalli           daltoni              dama        damarensis 
##                 2                 1                 2                 1 
##            dammah           darwini          dasyurus          dauricus 
##                 1                 1                 1                 1 
##          dauurica        davidianus      decemlineata             defua 
##                 1                 1                 1                 1 
##             degus        delectorum       delicatulus           delphis 
##                 1                 1                 1                 1 
##          demidoff      densirostris             denti    depressicornis 
##                 1                 1                 1                 1 
##         derbianus         derbyanus            derooi           deserti 
##                 2                 1                 1                 1 
##          desertor    desmarestianus             devia           diadema 
##                 1                 1                 1                 1 
##             diana            dianae             diazi        dichotomus 
##                 1                 1                 1                 1 
##        didactylus        difficilis            dispar           dobsoni 
##                 2                 1                 1                 1 
##        dolichurus           dolores            dorcas          dorsalis 
##                 1                 1                 1                 3 
##          dorsatum         douglasii       dromedarius             dugon 
##                 1                 1                 1                 1 
##  duodecimcostatus           duprasi        duvaucelii              ebii 
##                 1                 1                 1                 1 
##         ecaudatus             edeni         edwardsii           elaphus 
##                 1                 1                 1                 1 
##            elater             eldii           electra           elegans 
##                 1                 1                 1                 3 
##       elegantulus      elephantinus           ellioti    ellipsiprymnus 
##                 1                 1                 1                 1 
##             emini          entellus           equinus          eremicus 
##                 1                 1                 1                 1 
##           erminea      erythrogenys     erythroleucus        erythropus 
##                 1                 1                 1                 1 
##        erythrotis          etruscus        euphratica          europaea 
##                 1                 1                 1                 1 
##         europaeus         eurycerus          everetti        eversmanni 
##                 2                 1                 1                 1 
##       eversmannii            exilis           exulans         falconeri 
##                 1                 1                 1                 1 
##            fallax          fasciata         fasciatus      fascicularis 
##                 2                 2                 1                 1 
##            felina             ferox         ferrilata          fertilis 
##                 1                 1                 1                 1 
##             fiber            fieldi        fimbriatus        flavescens 
##                 1                 1                 1                 3 
##         flaviceps       flavicollis         flavigula      flaviventris 
##                 1                 1                 1                 1 
##    flavopunctatus       flavovittis            flavus         floridana 
##                 1                 1                 2                 1 
##        floridanus       fluviatilis           fodiens             foina 
##                 2                 1                 1                 1 
##          formosus          forresti          forsteri            fortis 
##                 1                 1                 1                 1 
##           fossana         francoisi        franklinii           frenata 
##                 1                 1                 1                 1 
##         frontalis           fulgens        fuliginosa        fulvescens 
##                 2                 1                 1                 1 
##       fulviventer       fulvorufula            fulvus           fumatus 
##                 1                 1                 2                 1 
##            fumeus          furcifer           fuscata         fusciceps 
##                 2                 1                 1                 1 
##       fuscicollis          fuscipes     fuscocapillus       fuscomurina 
##                 1                 2                 2                 1 
##            fuscus            gabbii     galapagoensis         galeritus 
##                 3                 1                 1                 1 
##         gambianus         gangetica           gapperi         garnettii 
##                 1                 1                 1                 1 
##           gazella             geata              geei            gelada 
##                 3                 1                 1                 1 
##           genetta        genibarbis       geoffrensis         geoffroyi 
##                 1                 1                 1                 3 
##         gerbillus           gibbsii          gigantea             gigas 
##                 1                 1                 1                 1 
##            glaber         glacialis             glama         glareolus 
##                 1                 1                 1                 1 
##          gleadowi         gliroides              glis              gnou 
##                 1                 2                 2                 1 
##           goeldii          goldmani           goliath             goral 
##                 1                 1                 1                 1 
##           gorilla          goslingi        gossypinus       gouazoupira 
##                 1                 1                 1                 1 
##          goudotii           gouldii   gracilicaudatus          gracilis 
##                 1                 1                 1                 1 
##       granatensis            granti            gratus          gregalis 
##                 1                 3                 1                 1 
##       gregorianus            grevyi           grimmia          griselda 
##                 1                 1                 1                 1 
##      griseoflavus           griseus      groenlandica     groenlandicus 
##                 1                 4                 1                 1 
##         grunniens            grypus           guairae          guanicoe 
##                 1                 1                 1                 1 
##               gud         guentheri           guereza              gulo 
##                 1                 2                 1                 1 
##             gundi         gunnisoni         gutturosa       gymnocercus 
##                 1                 1                 1                 1 
##           gymnura          gymnurus             haigi         hamadryas 
##                 1                 1                 1                 1 
##          harrisii           haydeni        heavisidii           hectori 
##                 1                 1                 1                 1 
##         heermanni          hemionus           henleyi hermannsburgensis 
##                 1                 2                 1                 1 
##    hermaphroditus          higginsi            hindei            hircus 
##                 1                 1                 2                 1 
##             hirta           hispida          hispidus         hodgsonii 
##                 1                 1                 4                 1 
##         hoffmanni           hookeri           hoolock           hooperi 
##                 1                 1                 1                 1 
##        horsfieldi             hosei       hottentotus              hoyi 
##                 1                 1                 2                 1 
##        hudsonicus         hudsonius       humeralifer       hummelincki 
##                 1                 2                 1                 1 
##           humulis           hunteri         hurrianae            hyaena 
##                 1                 1                 1                 1 
##          hybridus      hydrochaeris         hylocrius         hylophaga 
##                 1                 1                 1                 1 
##         hypomelas       hypoxanthus              ibex         ichneumon 
##                 1                 1                 1                 1 
##        idahoensis          imberbis           imhausi         imperator 
##                 1                 1                 1                 1 
##           inauris           inclusa          incomtus            indica 
##                 1                 1                 1                 6 
##           indicus             indri           inermis            ingens 
##                 1                 1                 1                 1 
##         ingrahami         inornatus          insignis         insularis 
##                 1                 1                 1                 1 
##       intermedius   interparietalis         interpres            intufi 
##                 2                 1                 1                 1 
##          inunguis         irroratus           jacchus          jacksoni 
##                 1                 2                 1                 1 
##           jaculus           janetta         japonicus          javanica 
##                 1                 1                 1                 1 
##         javanicus        jemlahicus            johnii         johnstoni 
##                 3                 1                 1                 1 
##           jubatus         juldaschi       kahuziensis           kaiseri 
##                 2                 1                 1                 1 
##          kappleri             kiang            kirkii           klossii 
##                 1                 1                 1                 1 
##               kob           krebsii          labiatus           lagopus 
##                 1                 1                 1                 1 
##        lagotricha           lagurus     lakedownensis          lamottei 
##                 1                 1                 1                 1 
##           laniger          lanigera               lar            largha 
##                 2                 1                 1                 1 
##           larvata          larvatus          lasiurus         lateralis 
##                 1                 1                 1                 1 
##      laticaudatus         latimanus           latrans            laucha 
##                 1                 2                 1                 1 
##             leche            lemmus       lemniscatus         lemurinus 
##                 1                 1                 1                 1 
##               leo           leonina            lepida           lepidus 
##                 1                 1                 1                 1 
##          leporina        leptoceros     leptodactylus          leptonyx 
##                 1                 1                 1                 1 
##            lervia            leucas          leucodon       leucogaster 
##                 1                 1                 2                 4 
##        leucogenys        leuconotus       leucophaeus          leucopus 
##                 1                 1                 1                 4 
##          leucoryx          leucotis          leucurus           levipes 
##                 1                 1                 2                 1 
##           lhoesti       liberiensis            libyca           libycus 
##                 1                 1                 1                 1 
##     lichtensteini    lichtensteinii           linsang        littoralis 
##                 1                 1                 1                 1 
##           lokriah     longicaudatus       longicaudis       longicaudus 
##                 1                 2                 1                 2 
##      longimembris        longipilis      longirostris            loriae 
##                 1                 1                 2                 1 
##             lotor             lowii      ludovicianus           lunatus 
##                 1                 2                 1                 1 
##             lupus       lusitanicus       luteogaster            luteus 
##                 1                 1                 1                 1 
##             lutra          lutreola         lutreolus            lutris 
##                 1                 1                 1                 1 
##              lynx            macaco     macrorhynchus          macrotis 
##                 1                 1                 1                 1 
##          macroura         macrourus          macrurus          maculata 
##                 2                 2                 1                 1 
##      maculicollis  madagascariensis        magnificus             maini 
##                 1                 1                 1                 1 
##             major         malayanus           manatus       maniculatus 
##                 2                 1                 1                 1 
##             manul         margarita         marginata       mariquensis 
##                 1                 1                 1                 1 
##         maritimus         marjorita         marmorata           marmota 
##                 1                 1                 1                 1 
##       marsupialis            martes        mastacalis           matacus 
##                 1                 1                 1                 1 
##             maura           maximus         maxwellii            mayori 
##                 1                 3                 1                 1 
##            medius      megacephalus         megaceros          megalops 
##                 1                 1                 1                 1 
##         megalotis    meinertzhageni        melalophos          melampus 
##                 2                 1                 1                 1 
##      melanocarpus       melanoleuca       melanophrys         melanotis 
##                 1                 1                 1                 2 
##         melanurus             melas             meles           meltada 
##                 1                 1                 1                 1 
##           meminna         menzbieri    mephistophiles          mephitis 
##                 1                 1                 1                 1 
##          mergulus        meridianus          merriami        mesoleucus 
##                 1                 1                 3                 1 
##         mesomelas         messorius          mexicana         mexicanus 
##                 2                 1                 1                 5 
##    microphthalmus           microps          micropus          microtis 
##                 1                 1                 3                 1 
##             midas       migratorius       mindorensis           minimus 
##                 1                 1                 1                 1 
##             minor        minutoides           minutus         mirabilis 
##                 3                 1                 2                 1 
##        mitchellii             mitis            miurus        mohavensis 
##                 1                 1                 1                 1 
##            moholi           molinae            mollis            moloch 
##                 1                 1                 1                 2 
##              mona          monachus             monax         moncktoni 
##                 1                 2                 1                 1 
##            mongoz         monoceros           montana          montanus 
##                 1                 1                 1                 2 
##        montebelli         monticola        monticolus      monticularis 
##                 1                 2                 1                 1 
##             morio          moschata         moschatus       moschiferus 
##                 1                 1                 2                 1 
##          muelleri           mulatta             mungo           muntjak 
##                 1                 1                 1                 1 
##           murinus        musculinus       musculoides          musculus 
##                 3                 1                 1                 2 
##        mustelinus       musteloides         myospalax        mystacalis 
##                 1                 1                 1                 1 
##        mystacinus            mystax        mysticetus            myurus 
##                 1                 2                 1                 1 
##             mzabi       namaquensis             nanus            napaea 
##                 1                 1                 3                 1 
##              napu            narica     nasomaculatus             nasua 
##                 1                 1                 1                 1 
##           nasutus        natalensis           nationi      nayaritensis 
##                 1                 2                 1                 1 
##            nayaur          nebulosa         neglectus           nelsoni 
##                 1                 1                 1                 2 
##           nemaeus        nemestrina         nictitans             niger 
##                 1                 1                 1                 3 
##             nigra        nigricauda       nigricollis        nigrifrons 
##                 1                 1                 2                 1 
##          nigripes      nigroviridis     nigrovittatus         niloticus 
##                 3                 1                 1                 1 
##            nippon          nitedula       nitratoides           nivalis 
##                 1                 1                 1                 2 
##          nivicola        niviventer         nolthenii             norae 
##                 1                 1                 1                 1 
##        norvegicus           notatus      novaeangliae   novaehollandiae 
##                 1                 1                 1                 1 
##      novemcinctus        nudicaudus          nuttalli         nuttallii 
##                 1                 1                 1                 1 
##            obesus       obliquidens          obscurus  ochraceocinereus 
##                 1                 1                 3                 1 
##         ochraceus       ochrogaster        ochrogenys      ochrognathus 
##                 1                 1                 1                 1 
##          ocularis         oeconomus           oedipus          oerstedi 
##                 1                 1                 1                 1 
##           ogilbyi         olivaceus           olympus              onca 
##                 1                 2                 1                 1 
##            opimus            oralis           orarius              orca 
##                 2                 1                 1                 1 
##             ordii           oregoni        oreotragus         oresterus 
##                 1                 1                 1                 1 
##        orientalis           ornatus              oryx             othus 
##                 1                 2                 1                 1 
##            ourebi           owstoni              paca         pacificus 
##                 1                 1                 1                 1 
##             pacos             paeba         paedulcus           pallasi 
##                 1                 1                 1                 1 
##          palliata         palliatus           pallida          pallidus 
##                 1                 1                 1                 1 
##          palmarum           palmeri       paludinosus         palustris 
##                 1                 1                 1                 3 
##      panamintinus          paniscus         paradoxus          pardalis 
##                 2                 2                 1                 1 
##        pardicolor          pardinus            pardus           parryii 
##                 1                 1                 1                 1 
##             parva         parvidens          parvipes           parvula 
##                 1                 1                 1                 1 
##            parvus         patagonum             patas            pecari 
##                 2                 1                 1                 1 
##        pectoralis             pelii       penicillata      penicillatus 
##                 1                 1                 2                 2 
##        peninsulae          pennanti         pennantii    pennsylvanicus 
##                 1                 1                 1                 1 
##      pentadactyla         percivali         peregusna         perfulvus 
##                 1                 1                 1                 1 
##       perpallidus          persicus         personata        personatus 
##                 1                 1                 1                 1 
##     perspicillata          peruanum          peruanus        petaurista 
##                 1                 1                 1                 1 
##           phayrei            phenax      philippensis      phocaenoides 
##                 1                 1                 1                 1 
##          phocoena         phyllotis          physalus            pichiy 
##                 1                 1                 1                 1 
##            pictus             pigra      pilligaensis         pilorides 
##                 2                 1                 1                 1 
##         pinchaque           pinetis         pinetorum          pithecia 
##                 1                 1                 1                 1 
##         planiceps        platythrix         platyurus           poensis 
##                 1                 1                 1                 1 
##          pogonias        polionotus           polulus         polykomos 
##                 1                 1                 1                 1 
##              pomo         porcellus          porcinus            porcus 
##                 1                 1                 1                 1 
##        potenziani             potto         praeconis           praetor 
##                 1                 1                 1                 1 
##         pratensis       prehensilis         prevostii          princeps 
##                 1                 2                 1                 2 
##      proboscideus      procyonoides         pruinosus              puda 
##                 1                 1                 1                 1 
##        pulchellum      pulverulenta            pumila           pumilio 
##                 1                 1                 1                 3 
##           pumilis          punctata           pusilla          pusillus 
##                 1                 1                 1                 2 
##          putorius          pygargus           pygmaea          pygmaeus 
##                 2                 3                 2                 3 
##         pyramidum        pyrenaicus      pyrrhorhinos          pyrropus 
##                 1                 1                 1                 1 
##      quadricornis   quadrimaculatus    quadrivittatus         quercinus 
##                 1                 1                 1                 1 
##            raddei           radiata         randensis            rattus 
##                 1                 1                 1                 1 
##       raviventris           redunca           reevesi          relictus 
##                 1                 1                 1                 1 
##    rhinogradoides       richardsoni      richardsonii       roborovskii 
##                 1                 2                 1                 1 
##           robusta          robustus           rosalia          rosmarus 
##                 1                 1                 1                 1 
##            rossii            roylei            rozeti           ruandae 
##                 1                 2                 1                 1 
##             rubex         rubicunda       rubiginosus       rubriventer 
##                 1                 1                 1                 1 
##             ruddi         rueppelli              rufa         rufescens 
##                 1                 1                 1                 3 
##      ruficaudatus        ruficaudus         rufifrons         rufilatus 
##                 1                 1                 1                 1 
##            rufina      rufobrachium         rufocanus             rufus 
##                 1                 1                 1                 4 
##         rupestris         rupicapra          russatus           russula 
##                 3                 1                 1                 1 
##            rutila          rutilans           rutilus        sabanicola 
##                 1                 1                 1                 1 
##          sabrinus           sagitta        salinicola          saltiana 
##                 1                 1                 1                 1 
##         salvanius           salvini         sanguinea           sapidus 
##                 1                 1                 1                 1 
##           satanas         saturatus         saxatilis     schauinslandi 
##                 2                 1                 1                 1 
##      schisticolor          sciureus          scriptus            scrofa 
##                 1                 1                 1                 1 
##           selousi      semispinosus      semistriatus      senegalensis 
##                 1                 2                 1                 2 
##             senex         seniculus     septemcinctus            serval 
##                 1                 1                 1                 1 
##           setosus           setzeri             sevia        sexcinctus 
##                 2                 1                 1                 1 
##             shawi       shortridgei          sibirica         sibiricus 
##                 1                 1                 4                 2 
##          sikapusi           silenus        silvestris       silvicultor 
##                 1                 1                 1                 1 
##          simensis            simoni             simum             simus 
##                 1                 1                 1                 1 
##            sinica             sinus          siskiyou         sitkensis 
##                 1                 1                 1                 1 
##         sloggetti          socialis     soemmerringii           solatus 
##                 1                 1                 1                 1 
##         sondaicus           sonomae          sordidus         speciosus 
##                 1                 1                 1                 1 
##       spectabilis          spectrum            spekei            spekii 
##                 1                 1                 1                 1 
##            sphinx         spilosoma            spixii         splendens 
##                 1                 1                 1                 1 
##           spretus         squamipes            steini            stella 
##                 1                 1                 1                 1 
##         stephensi         strelzowi      strepsiceros          striatus 
##                 2                 1                 1                 3 
##        stuhlmanni        suaveolens         subflavus      subgutturosa 
##                 1                 1                 1                 1 
##       sublineatus      subterraneus           suillus      sumatraensis 
##                 1                 1                 2                 1 
##       sumatrensis       sumichrasti          sungorus         suricatta 
##                 2                 2                 1                 1 
##          suslicus      swinderianus          sylvanus        sylvaticus 
##                 1                 1                 1                 1 
##        sylvestris       syndactylus          syrichta            tajacu 
##                 1                 1                 1                 1 
##          talapoin           talarum          talazaci          talpinus 
##                 1                 1                 1                 1 
##         talpoides      tamariscinus              tana          tarandus 
##                 2                 1                 1                 1 
##       tardigradus          tatarica       tattersalli          taurinus 
##                 1                 1                 1                 1 
##         taxicolor             taxus           taylori           teguina 
##                 1                 1                 1                 1 
##          telfairi             telum        temminckii          tenuipes 
##                 1                 1                 2                 1 
##            tenuis      tereticaudus        terrestris      tetradactyla 
##                 1                 1                 2                 3 
##     tetradactylus         thibetana        thibetanus           thomasi 
##                 1                 1                 1                 1 
##         thomsonii             thous           tigrina          tigrinus 
##                 1                 1                 1                 1 
##            tigris           timidus        timorensis        tiomanicus 
##                 1                 1                 1                 1 
##             tolai         torquatus          torridus        townsendii 
##                 1                 5                 1                 6 
##      tragocamelus     transcaspicus    transitionalis         tricuspis 
##                 1                 1                 1                 1 
##        tridactyla       tridactylus  tridecemlineatus        trinotatus 
##                 1                 1                 1                 1 
##         tristrami            triton        trivirgata       trivirgatus 
##                 1                 1                 1                 1 
##       troglodytes        tropicalis       trowbridgii             truei 
##                 1                 1                 1                 1 
##         truncatus          tschudii         tullbergi           tunneyi 
##                 1                 1                 1                 1 
##             turba       turcmenicus            typica           typicus 
##                 1                 1                 1                 1 
##             typus           tytonis          umbrinus      unalascensis 
##                 2                 1                 1                 1 
##             uncia         undulatus            ungava      unguiculatus 
##                 1                 1                 1                 1 
##          unicolor         unicornis       univittatus         uralensis 
##                 1                 1                 1                 1 
##            urichi           ursinus           vagrans              vali 
##                 1                 2                 1                 1 
##            valida    vancouverensis          vardonii         variegata 
##                 1                 1                 1                 1 
##        variegatus           varilla            varius             vates 
##                 3                 1                 2                 1 
##             velox         venaticus          venustus         verreauxi 
##                 2                 1                 2                 1 
##             verus           vetulus        vexillifer            viaria 
##                 1                 1                 1                 1 
##           vicugna            vignei     villosissimus          villosus 
##                 1                 1                 1                 3 
##       vinogradovi       virginianus          viscacia             vison 
##                 1                 1                 1                 1 
##           vittata          vitulina        viverrinus            volans 
##                 1                 1                 1                 3 
##       vordermanni          vulgaris            vulpes           wagneri 
##                 1                 1                 1                 1 
##           walleri       washingtoni         weddellii            wiedii 
##                 1                 1                 1                 1 
##           wilsoni             wolfi         woodwardi          woosnami 
##                 1                 1                 1                 2 
##            wynnei         xanthipes     xanthognathus      xerampelinus 
##                 1                 1                 1                 1 
##        yaguarondi      yucatanensis       yucatanicus      zanzibaricus 
##                 1                 1                 1                 1 
##             zebra           zenkeri             zerda       zeylonensis 
##                 2                 1                 1                 1 
##         zibellina           zibetha        zibethicus 
##                 1                 1                 1
```

## Wrap-up
Please review the learning goals and be sure to use the code here as a reference when completing the homework.  
-->[Home](https://jmledford3115.github.io/datascibiol/)
