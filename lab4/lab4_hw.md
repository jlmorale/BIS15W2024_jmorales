---
title: "Lab 4 Homework"
author: "Jocelyn Morales"
date: "2024-01-29"
output:
  html_document: 
    theme: spacelab
    keep_md: true
---



## Instructions

Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!

## Load the tidyverse


```r
library(tidyverse)
```

## Data

For the homework, we will use data about vertebrate home range sizes. The data are in the class folder, but the reference is below.

**Database of vertebrate home range sizes.**\
Reference: Tamburello N, Cote IM, Dulvy NK (2015) Energy and the scaling of animal space use. The American Naturalist 186(2):196-211. <http://dx.doi.org/10.1086/682070>.\
Data: <http://datadryad.org/resource/doi:10.5061/dryad.q5j65/1>

**1. Load the data into a new object called `homerange`.**


```r
homerange <- read.csv("data/Tamburelloetal_HomeRangeDatabase.csv")
```

**2. Explore the data. Show the dimensions, column names, classes for each variable, and a statistical summary. Keep these as separate code chunks.**


```r
dim(homerange)
```

```
## [1] 569  24
```


```r
names(homerange)
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```


```r
summary(homerange)
```

```
##     taxon           common.name           class              order          
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##     family             genus             species          primarymethod     
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##       N              mean.mass.g        log10.mass     
##  Length:569         Min.   :      0   Min.   :-0.6576  
##  Class :character   1st Qu.:     50   1st Qu.: 1.6990  
##  Mode  :character   Median :    330   Median : 2.5185  
##                     Mean   :  34602   Mean   : 2.5947  
##                     3rd Qu.:   2150   3rd Qu.: 3.3324  
##                     Max.   :4000000   Max.   : 6.6021  
##                                                        
##  alternative.mass.reference  mean.hra.m2          log10.hra     
##  Length:569                 Min.   :0.000e+00   Min.   :-1.523  
##  Class :character           1st Qu.:4.500e+03   1st Qu.: 3.653  
##  Mode  :character           Median :3.934e+04   Median : 4.595  
##                             Mean   :2.146e+07   Mean   : 4.709  
##                             3rd Qu.:1.038e+06   3rd Qu.: 6.016  
##                             Max.   :3.551e+09   Max.   : 9.550  
##                                                                 
##  hra.reference         realm           thermoregulation    locomotion       
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  trophic.guild       dimension            preymass         log10.preymass   
##  Length:569         Length:569         Min.   :     0.67   Min.   :-0.1739  
##  Class :character   Class :character   1st Qu.:    20.02   1st Qu.: 1.3014  
##  Mode  :character   Mode  :character   Median :    53.75   Median : 1.7304  
##                                        Mean   :  3989.88   Mean   : 2.0188  
##                                        3rd Qu.:   363.35   3rd Qu.: 2.5603  
##                                        Max.   :130233.20   Max.   : 5.1147  
##                                        NA's   :502         NA's   :502      
##       PPMR         prey.size.reference
##  Min.   :  0.380   Length:569         
##  1st Qu.:  3.315   Class :character   
##  Median :  7.190   Mode  :character   
##  Mean   : 31.752                      
##  3rd Qu.: 15.966                      
##  Max.   :530.000                      
##  NA's   :502
```


```r
str(homerange)
```

```
## 'data.frame':	569 obs. of  24 variables:
##  $ taxon                     : chr  "lake fishes" "river fishes" "river fishes" "river fishes" ...
##  $ common.name               : chr  "american eel" "blacktail redhorse" "central stoneroller" "rosyside dace" ...
##  $ class                     : chr  "actinopterygii" "actinopterygii" "actinopterygii" "actinopterygii" ...
##  $ order                     : chr  "anguilliformes" "cypriniformes" "cypriniformes" "cypriniformes" ...
##  $ family                    : chr  "anguillidae" "catostomidae" "cyprinidae" "cyprinidae" ...
##  $ genus                     : chr  "anguilla" "moxostoma" "campostoma" "clinostomus" ...
##  $ species                   : chr  "rostrata" "poecilura" "anomalum" "funduloides" ...
##  $ primarymethod             : chr  "telemetry" "mark-recapture" "mark-recapture" "mark-recapture" ...
##  $ N                         : chr  "16" NA "20" "26" ...
##  $ mean.mass.g               : num  887 562 34 4 4 ...
##  $ log10.mass                : num  2.948 2.75 1.531 0.602 0.602 ...
##  $ alternative.mass.reference: chr  NA NA NA NA ...
##  $ mean.hra.m2               : num  282750 282.1 116.1 125.5 87.1 ...
##  $ log10.hra                 : num  5.45 2.45 2.06 2.1 1.94 ...
##  $ hra.reference             : chr  "Minns, C. K. 1995. Allometry of home range size in lake and river fishes. Canadian Journal of Fisheries and Aquatic Sciences 52 "Minns, C. K. 1995. Allometry of home range size in lake and river fishes. Canadian Journal of Fisheries and Aquatic Sciences 52 "Minns, C. K. 1995. Allometry of home range size in lake and river fishes. Canadian Journal of Fisheries and Aquatic Sciences 52 "Minns, C. K. 1995. Allometry of home range size in lake and river fishes. Canadian Journal of Fisheries and Aquatic Sciences 52 ...
##  $ realm                     : chr  "aquatic" "aquatic" "aquatic" "aquatic" ...
##  $ thermoregulation          : chr  "ectotherm" "ectotherm" "ectotherm" "ectotherm" ...
##  $ locomotion                : chr  "swimming" "swimming" "swimming" "swimming" ...
##  $ trophic.guild             : chr  "carnivore" "carnivore" "carnivore" "carnivore" ...
##  $ dimension                 : chr  "3D" "2D" "2D" "2D" ...
##  $ preymass                  : num  NA NA NA NA NA NA 1.39 NA NA NA ...
##  $ log10.preymass            : num  NA NA NA NA NA ...
##  $ PPMR                      : num  NA NA NA NA NA NA 530 NA NA NA ...
##  $ prey.size.reference       : chr  NA NA NA NA ...
```

**3. Change the class of the variables `taxon` and `order` to factors and display their levels.**


```r
homerange$taxon <- as.factor(homerange$taxon)
homerange$order <- as.factor(homerange$order)
```


```r
levels(homerange$taxon)
```

```
## [1] "birds"         "lake fishes"   "lizards"       "mammals"      
## [5] "marine fishes" "river fishes"  "snakes"        "tortoises"    
## [9] "turtles"
```

```r
levels(homerange$order)
```

```
##  [1] "accipitriformes"       "afrosoricida"          "anguilliformes"       
##  [4] "anseriformes"          "apterygiformes"        "artiodactyla"         
##  [7] "caprimulgiformes"      "carnivora"             "charadriiformes"      
## [10] "columbidormes"         "columbiformes"         "coraciiformes"        
## [13] "cuculiformes"          "cypriniformes"         "dasyuromorpha"        
## [16] "dasyuromorpia"         "didelphimorphia"       "diprodontia"          
## [19] "diprotodontia"         "erinaceomorpha"        "esociformes"          
## [22] "falconiformes"         "gadiformes"            "galliformes"          
## [25] "gruiformes"            "lagomorpha"            "macroscelidea"        
## [28] "monotrematae"          "passeriformes"         "pelecaniformes"       
## [31] "peramelemorphia"       "perciformes"           "perissodactyla"       
## [34] "piciformes"            "pilosa"                "proboscidea"          
## [37] "psittaciformes"        "rheiformes"            "roden"                
## [40] "rodentia"              "salmoniformes"         "scorpaeniformes"      
## [43] "siluriformes"          "soricomorpha"          "squamata"             
## [46] "strigiformes"          "struthioniformes"      "syngnathiformes"      
## [49] "testudines"            "tetraodontiformes\xa0" "tinamiformes"
```

**4. What taxa are represented in the `homerange` data frame? Make a new data frame `taxa` that is restricted to taxon, common name, class, order, family, genus, species.**


```r
taxa <- select(homerange, "taxon", "common.name", "class", "order", "family", "genus", "species")
```

**5. The variable `taxon` identifies the common name groups of the species represented in `homerange`. Make a table the shows the counts for each of these `taxon`.**


```r
table(taxa$taxon)
```

```
## 
##         birds   lake fishes       lizards       mammals marine fishes 
##           140             9            11           238            90 
##  river fishes        snakes     tortoises       turtles 
##            14            41            12            14
```

**6. The species in `homerange` are also classified into trophic guilds. How many species are represented in each trophic guild.**


```r
table(homerange$trophic.guild)
```

```
## 
## carnivore herbivore 
##       342       227
```

Just do questions 1-6 due by Jan 25.

Questions 7-10 finish during class (Jan 25)

**7. Make two new data frames, one which is restricted to carnivores and another that is restricted to herbivores.**


```r
carnivores <- filter(homerange, trophic.guild=="carnivore")
```


```r
herbivores <- filter(homerange, trophic.guild=="herbivore")
```

**8. Do herbivores or carnivores have, on average, a larger `mean.hra.m2`? Remove any NAs from the data.**


```r
mean(carnivores$mean.hra.m2)
```

```
## [1] 13039918
```


```r
mean(herbivores$mean.hra.m2)
```

```
## [1] 34137012
```

**9. Make a new data frame `owls` that is limited to the mean mass, log10 mass, family, genus, and species of owls in the database. Which is the smallest owl? What is its common name? Do a little bit of searching online to see what you can learn about this species and provide a link below**


```r
owls <- select(homerange, "mean.mass.g", "log10.mass", "family", "genus", "species")
filter(homerange, order=="strigiformes")
```

```
##   taxon        common.name class        order    family      genus     species
## 1 birds         boreal owl  aves strigiformes strigidae   aegolius    funereus
## 2 birds     long-eared owl  aves strigiformes strigidae       asio        otus
## 3 birds         little owl  aves strigiformes strigidae     athene      noctua
## 4 birds Eurasian eagle-owl  aves strigiformes strigidae       bubo        bubo
## 5 birds   great horned owl  aves strigiformes strigidae       bubo virginianus
## 6 birds Eurasian pygmy owl  aves strigiformes strigidae glaucidium  passerinum
## 7 birds          snowy owl  aves strigiformes strigidae     nyctea   scandiaca
## 8 birds          tawny owl  aves strigiformes strigidae      strix       aluco
## 9 birds           barn owl  aves strigiformes tytonidae       tyto        alba
##        primarymethod    N mean.mass.g log10.mass alternative.mass.reference
## 1         telemetry* <NA>      119.00   2.075547                       <NA>
## 2         telemetry* <NA>      252.00   2.401401                       <NA>
## 3         telemetry* <NA>      156.50   2.194514                       <NA>
## 4         telemetry* <NA>     2191.00   3.340642                       <NA>
## 5 direct observation <NA>     1510.00   3.178977                       <NA>
## 6         telemetry* <NA>       61.32   1.787602                       <NA>
## 7 direct observation <NA>     1920.00   3.283301                       <NA>
## 8 direct observation   55      519.00   2.715167                       <NA>
## 9         telemetry* <NA>      285.00   2.454845                       <NA>
##   mean.hra.m2 log10.hra
## 1   3140000.0  6.496930
## 2  19620000.0  7.292699
## 3    500000.0  5.698970
## 4  16000000.0  7.204120
## 5   2124596.2  6.327276
## 6   1250000.0  6.096910
## 7   4937157.0  6.693477
## 8    356932.2  5.552586
## 9   1500000.0  6.176091
##                                                                                                                                                                            hra.reference
## 1 Ottaviani, D., S. C. Cairns, M. Oliverio, and L. Boitani. 2006. Body mass as a predictive variable of home-range size among Italian mammals and birds. Journal of Zoology 269:317-330.
## 2 Ottaviani, D., S. C. Cairns, M. Oliverio, and L. Boitani. 2006. Body mass as a predictive variable of home-range size among Italian mammals and birds. Journal of Zoology 269:317-330.
## 3 Ottaviani, D., S. C. Cairns, M. Oliverio, and L. Boitani. 2006. Body mass as a predictive variable of home-range size among Italian mammals and birds. Journal of Zoology 269:317-330.
## 4 Ottaviani, D., S. C. Cairns, M. Oliverio, and L. Boitani. 2006. Body mass as a predictive variable of home-range size among Italian mammals and birds. Journal of Zoology 269:317-330.
## 5                                                                                                    Schoener, T. W. 1968. Sizes of feeding territories among birds. Ecology 49:123-141.
## 6 Ottaviani, D., S. C. Cairns, M. Oliverio, and L. Boitani. 2006. Body mass as a predictive variable of home-range size among Italian mammals and birds. Journal of Zoology 269:317-330.
## 7                                                                                                    Schoener, T. W. 1968. Sizes of feeding territories among birds. Ecology 49:123-141.
## 8                                                                                                    Schoener, T. W. 1968. Sizes of feeding territories among birds. Ecology 49:123-141.
## 9 Ottaviani, D., S. C. Cairns, M. Oliverio, and L. Boitani. 2006. Body mass as a predictive variable of home-range size among Italian mammals and birds. Journal of Zoology 269:317-330.
##         realm thermoregulation locomotion trophic.guild dimension preymass
## 1 terrestrial        endotherm     flying     carnivore        3D       NA
## 2 terrestrial        endotherm     flying     carnivore        3D    32.98
## 3 terrestrial        endotherm     flying     carnivore        3D    20.66
## 4 terrestrial        endotherm     flying     carnivore        3D   375.00
## 5 terrestrial        endotherm     flying     carnivore        3D   279.11
## 6 terrestrial        endotherm     flying     carnivore        3D    16.99
## 7 terrestrial        endotherm     flying     carnivore        3D       NA
## 8 terrestrial        endotherm     flying     carnivore        3D    29.61
## 9 terrestrial        endotherm     flying     carnivore        3D    19.39
##   log10.preymass      PPMR
## 1             NA        NA
## 2       1.518251  7.640000
## 3       1.315130  7.575700
## 4       2.574031  5.842667
## 5       2.445775  5.410000
## 6       1.230193  3.610000
## 7             NA        NA
## 8       1.471438 17.530000
## 9       1.287578 14.700000
##                                                                                                                                                                                                                                    prey.size.reference
## 1                                                                                                                                                                                                                                                 <NA>
## 2 Jaksic FM, Delibes M.1987. A Comparative Analysis of Food-Niche Relationships and Trophic Guild Structure in TwoAssemblages of Vertebrate Predators Differing in Species Richness: Causes, Correlations, and Consequences. Oecologia 71(3), 461-472.
## 3 Jaksic FM, Delibes M.1987. A Comparative Analysis of Food-Niche Relationships and Trophic Guild Structure in TwoAssemblages of Vertebrate Predators Differing in Species Richness: Causes, Correlations, and Consequences. Oecologia 71(3), 461-472.
## 4                                                                                                  Marchesi L, Sergio F, Pedrini P. 2002. Costs and benefits of breeding in human-altered landscapes for the Eagle Owl Bubo bubo. Ibis 144, E164-E177.
## 5                                                                                          Jaksic FM, Carothers JH. 1985. Ecological, Morphological, and Bioenergetic Correlates of Hunting Mode in Hawks and Owls. Ornis Scandinavica 16(3), 165-172.
## 6                                                                                    Slagsvold T, Sonerud GA. 2007. Prey size and ingestion rate in raptors: importance for sex roles and reversed sexual size dimorphism. J. Avian Biol. 38: 650 661.
## 7                                                                                                                                                                                                                                                 <NA>
## 8                                                                                  Galeotti P, Morimando F, Violani C. 2009. Feeding ecology of the tawny owls (Strix aluco) in urban habitats (northern Italy). Bolletino di zoologia 58(2), 143-150.
## 9  Jaksic FM, Delibes M.1987. A Comparative Analysis of Food-Niche Relationships and Trophic Guild Structure in TwoAssemblages of Vertebrate Predators Differing in Species Richness: Causes, Correlations, andConsequences. Oecologia 71(3), 461-472.
```


```r
filter(homerange, mean.mass.g==61.32)
```

```
##   taxon        common.name class        order    family      genus    species
## 1 birds Eurasian pygmy owl  aves strigiformes strigidae glaucidium passerinum
##   primarymethod    N mean.mass.g log10.mass alternative.mass.reference
## 1    telemetry* <NA>       61.32   1.787602                       <NA>
##   mean.hra.m2 log10.hra
## 1     1250000   6.09691
##                                                                                                                                                                            hra.reference
## 1 Ottaviani, D., S. C. Cairns, M. Oliverio, and L. Boitani. 2006. Body mass as a predictive variable of home-range size among Italian mammals and birds. Journal of Zoology 269:317-330.
##         realm thermoregulation locomotion trophic.guild dimension preymass
## 1 terrestrial        endotherm     flying     carnivore        3D    16.99
##   log10.preymass PPMR
## 1       1.230193 3.61
##                                                                                                                                                 prey.size.reference
## 1 Slagsvold T, Sonerud GA. 2007. Prey size and ingestion rate in raptors: importance for sex roles and reversed sexual size dimorphism. J. Avian Biol. 38: 650 661.
```

The Eurasian pygmy owl is the smallest owl in Europe. This is a website with more information of the owl. [Animal Diversity Web](https://animaldiversity.org/accounts/Glaucidium_passerinum/) 

**10. As measured by the data, which bird species has the largest home range? Show all of your work, please. Look this species up online and tell me about it!**.


```r
largest_homerange <- select(homerange, "common.name" , "class", "species", "mean.hra.m2", "log10.hra")
```


```r
largest_homerange %>%
  filter(class=="aves") %>%
  arrange(desc(mean.hra.m2))
```

```
##                        common.name class         species  mean.hra.m2 log10.hra
## 1                         caracara  aves        cheriway 241000000.00  8.382017
## 2                Montagu's harrier  aves        pygargus 200980000.00  8.303153
## 3                 peregrine falcon  aves      peregrinus 153860000.00  8.187126
## 4                     booted eagle  aves        pennatus 117300000.00  8.069298
## 5                          ostrich  aves         camelus  84300000.00  7.925828
## 6           short-toed snake eagle  aves        gallicus  78500000.00  7.894870
## 7             European turtle dove  aves          turtur  63585000.00  7.803355
## 8                 Egyptian vulture  aves    percnopterus  63570000.00  7.803252
## 9                   common buzzard  aves           buteo  50240000.00  7.701050
## 10                   lanner falcon  aves       biarmicus  50000000.00  7.698970
## 11                         gadwall  aves        strepera  45912000.00  7.661926
## 12                Northern goshawk  aves        gentilis  40000000.00  7.602060
## 13                   common cuckoo  aves         canorus  38460000.00  7.585009
## 14                    common raven  aves           corax  28000000.00  7.447158
## 15                    golden eagle  aves      chrysaetos  27550000.00  7.440122
## 16                  prairie falcon  aves       mexicanus  25778434.50  7.411257
## 17                     lesser rhea  aves         pennata  23880000.00  7.378034
## 18                        red kite  aves          milvus  19625000.00  7.292810
## 19                 Bonelli's eagle  aves       fasciatus  19620000.00  7.292699
## 20                  long-eared owl  aves            otus  19620000.00  7.292699
## 21                     sage grouse  aves    urophasianus  18158215.95  7.259073
## 22              Eurasian eagle-owl  aves            bubo  16000000.00  7.204120
## 23                          hoopoe  aves           epops  12560000.00  7.098990
## 24            great spotted cuckoo  aves      glandarius  12560000.00  7.098990
## 25         greater prairie-chicken  aves cupido pinnatus  12030000.00  7.080266
## 26            Eurasian sparrowhawk  aves           nisus   7100000.00  6.851258
## 27            western capercaillie  aves       urogallus   5500000.00  6.740363
## 28         white-backed woodpecker  aves        leucotos   5306600.00  6.724816
## 29                       snowy owl  aves       scandiaca   4937157.00  6.693477
## 30          grey-headed woodpecker  aves           canus   4521600.00  6.655292
## 31                 red-tailed hawk  aves     jamaicensis   4249192.50  6.628306
## 32                black woodpecker  aves         martius   3500000.00  6.544068
## 33                   common linnet  aves       cannabina   3140000.00  6.496930
## 34                      boreal owl  aves        funereus   3140000.00  6.496930
## 35                European kestrel  aves     tinnunculus   3000000.00  6.477121
## 36              common wood pigeon  aves        palumbus   2540000.00  6.404834
## 37                     hen harrier  aves         cyaneus   2521187.55  6.401605
## 38                 Swainson's hawk  aves       swainsoni   2464531.65  6.391734
## 39                   oystercatcher  aves      ostralegus   2460000.00  6.390935
## 40                    greater rhea  aves       americana   2450000.00  6.389166
## 41                   Cooper's hawk  aves        cooperii   2254095.45  6.352972
## 42                great horned owl  aves     virginianus   2124596.25  6.327276
## 43                    black grouse  aves          tetrix   1975000.00  6.295567
## 44       European green woodpecker  aves         viridis   1850000.00  6.267172
## 45                        barn owl  aves            alba   1500000.00  6.176091
## 46                American kestrel  aves      sparverius   1416397.50  6.151185
## 47              Eurasian pygmy owl  aves      passerinum   1250000.00  6.096910
## 48                Eurasian wryneck  aves       torquilla   1038100.00  6.016239
## 49                 European roller  aves        garrulus   1000000.00  6.000000
## 50              sharp-shinned hawk  aves        striatus    995525.10  5.998052
## 51               European nightjar  aves       europaeus    785000.00  5.894870
## 52                   white wagtail  aves            alba    785000.00  5.894870
## 53           red-throated caracara  aves      americanus    666000.00  5.823474
## 54             red-shouldered hawk  aves        lineatus    639402.30  5.805774
## 55              lesser grey shrike  aves           minor    635800.00  5.803321
## 56              greater roadrunner  aves   californianus    550000.00  5.740363
## 57                      little owl  aves          noctua    500000.00  5.698970
## 58            banded ground-cuckoo  aves      radiolosus    499000.00  5.698101
## 59             northern brown kiwi  aves       australis    463900.00  5.666424
## 60                       tawny owl  aves           aluco    356932.17  5.552586
## 61  Eurasian three-toed woodpecker  aves     tridactylus    350000.00  5.544068
## 62                          kakapo  aves     habroptilus    195000.00  5.290035
## 63                   great bittern  aves       stellaris    193000.00  5.285557
## 64      middle spotted woodpeckers  aves          medius    141500.00  5.150756
## 65              spotted nutcracker  aves   caryocatactes    132332.00  5.121665
## 66                    hazel grouse  aves         bonasia    103000.00  5.012837
## 67                   least bittern  aves          exilis     97000.00  4.986772
## 68          tooth-billed bowerbird  aves    dentirostris     95000.00  4.977724
## 69                 brown wood rail  aves           wolfi     90000.00  4.954243
## 70                eastern kingbird  aves        tyrannus     83769.80  4.923087
## 71                        woodlark  aves         arborea     82960.43  4.918871
## 72                 woodchat shrike  aves         senator     80000.00  4.903090
## 73               loggerhead shrike  aves    ludovicianus     75676.10  4.878959
## 74                  grey partridge  aves          perdix     62000.00  4.792392
## 75        red-throated ant tanager  aves      fuscicauda     60702.75  4.783208
## 76         red-crowned ant tanager  aves          rubica     48562.20  4.686298
## 77            Eurasian treecreeper  aves      familiaris     47000.00  4.672098
## 78              eastern wood pewee  aves          virens     44029.73  4.643746
## 79                       king rail  aves         elegans     44000.00  4.643453
## 80                       corncrake  aves            crex     43000.00  4.633468
## 81                 long-tailed tit  aves        caudatus     42000.00  4.623249
## 82                common chaffinch  aves         coelebs     42000.00  4.623249
## 83       Western Bonelli's warbler  aves         bonelli     35000.00  4.544068
## 84              Kirtland's warbler  aves       kirtlandi     33993.54  4.531396
## 85            Peruvian plantcutter  aves       raimondii     30900.00  4.489958
## 86                chipping sparrow  aves       passerina     30756.06  4.487931
## 87              eastern meadowlark  aves           magna     30351.38  4.482178
## 88              western meadowlard  aves        neglecta     30351.38  4.482178
## 89               melodious warbler  aves      polyglotta     30000.00  4.477121
## 90                willow ptarmigan  aves         lagopus     25899.84  4.413297
## 91                   canyon towhee  aves          fuscus     25899.84  4.413297
## 92                    Oak titmouse  aves       inornatus     24281.10  4.385268
## 93                  ornate tinamou  aves          ornata     24281.10  4.385268
## 94                       marsh tit  aves       palustris     22662.36  4.355305
## 95               European nuthatch  aves        europaea     21000.00  4.322219
## 96                       goldcrest  aves         regulus     19900.00  4.298853
## 97                    dusky grouse  aves        obscurus     16996.77  4.230366
## 98           American tree sparrow  aves         arborea     16996.77  4.230366
## 99                common firecrest  aves    ignicapillus     16500.00  4.217484
## 100                 Abert's towhee  aves          aberti     16187.40  4.209177
## 101              red-backed shrike  aves        collurio     15782.72  4.198182
## 102       American gray flycatcher  aves        wrightii     15782.72  4.198182
## 103              northern wheatear  aves        oenanthe     15378.03  4.186901
## 104             Carolina chickadee  aves    carolinensis     14973.35  4.175319
## 105           prothonotary warbler  aves          citrea     14973.35  4.175319
## 106             black-capped vireo  aves    atricapillus     14973.35  4.175319
## 107         black-capped chickadee  aves    atricapillus     14568.66  4.163420
## 108       streaked fantail warbler  aves        juncidis     14400.00  4.158362
## 109                   Bell's vireo  aves           belli     11735.87  4.069515
## 110            grasshopper sparrow  aves      savannarum     10926.50  4.038481
## 111         western yellow wagtail  aves           flava     10117.13  4.005057
## 112                       ovenbird  aves    aurocapillus     10117.13  4.005057
## 113                 Canada warbler  aves      canadensis     10117.13  4.005057
## 114                  Eurasian wren  aves     troglodytes     10117.13  4.005057
## 115               eastern bluebird  aves          sialis     10117.13  4.005057
## 116                 European serin  aves         serinus     10000.00  4.000000
## 117             spotted flycatcher  aves         striata     10000.00  4.000000
## 118               mourning warbler  aves    philadelphia      7689.02  3.885871
## 119                       whinchat  aves         rubetra      7300.00  3.863323
## 120               magnolia warbler  aves        magnolia      7284.33  3.862390
## 121                 red-eyed vireo  aves       olivaceus      7284.33  3.862390
## 122   black-throated green warbler  aves          virens      6474.96  3.811237
## 123         chestnut-sided warbler  aves    pensylvanica      6070.28  3.783209
## 124            common yellowthroat  aves         trichas      5260.91  3.721061
## 125           Blackburnian warbler  aves           fusca      5260.91  3.721061
## 126                 Berwick's wren  aves        bewickiI      4856.22  3.686298
## 127                common redstart  aves     phoenicurus      4500.00  3.653213
## 128           northern mockingbird  aves     polyglottos      4046.85  3.607117
## 129                     house wren  aves           aedon      4046.85  3.607117
## 130              Marmora's warbler  aves           sarda      3300.00  3.518514
## 131                        wrentit  aves        fasciata      3237.48  3.510207
## 132               Dartford warbler  aves          undata      2800.00  3.447158
## 133                      inca dove  aves            inca      2589.98  3.413296
## 134              American redstart  aves       ruticilla      1942.49  3.288359
## 135               least flycatcher  aves         minimus      1780.61  3.250569
## 136        American yellow warbler  aves        petechia      1699.68  3.230367
## 137           yellow-breasted chat  aves          virens      1335.46  3.125631
## 138               white-eyed vireo  aves         griseus      1335.46  3.125631
## 139                  Carolina wren  aves    ludovicianus      1214.06  3.084240
## 140                 indigo bunting  aves          cyanea      1052.18  3.022090
```
The bird with the largest home range is the Caracara with a mean home range area of 241000000.00. 

The Crested Caracara is related to the typical falcons that live in the regions of Florida, Southeast, Southwest, and Texas. [Crested Caracara](https://www.audubon.org/field-guide/bird/crested-caracara)

## Push your final code to GitHub!

Please be sure that you check the `keep md` file in the knit preferences. 
