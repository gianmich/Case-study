## Case study
========================================================

_Das ist eine Übung damit ich "tidy data" lerne._


First step is to load the libraries we need:


```r
library(reshape2)
library(ggplot2)
library(plyr)
library(stringr)
library(MASS)
library(ProjectTemplate)
```


Ich benutze library(ProjectTemplate) um mein Project besser zu organisieren. 


```r
create.project(CaseStudy)
```

```
## Error: object 'CaseStudy' not found
```

```r
setwd("~/CaseStudy")
```

xtable.r in die Folgende directory. Dann habe ich die Package xtable installiert


```r
source("~/Documents/Doktorarbeit/xtable.r")
```

Download .csv Datei von https://github.com/hadley/mexico-mortality/raw/master/deaths/deaths08.csv.bz2
and placed it in ~/CaseStudy


```r
load.project()
```

```
## Loading project configuration
```

```
## Error: You are missing a configuration file: config/global.dcf
```

```r
deaths <- deaths08
```

```
## Error: object 'deaths08' not found
```







You can also embed plots, for example:


```r
plot(cars)
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5.png) 


