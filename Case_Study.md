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
library(Hmisc)
```

```
## Loading required package: grid
## Loading required package: lattice
## Loading required package: survival
## Loading required package: splines
## Loading required package: Formula
## 
## Attaching package: 'Hmisc'
## 
## The following objects are masked from 'package:plyr':
## 
##     is.discrete, summarize
## 
## The following objects are masked from 'package:base':
## 
##     format.pval, round.POSIXt, trunc.POSIXt, units
```

```r
library(knitr)
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

```
## 
## Attaching package: 'xtable'
## 
## The following objects are masked from 'package:Hmisc':
## 
##     label, label<-
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


Jetzt möchte ich mich mit den Totesfällen an bestimmten Tageszeiten beschäftigen.
Mit foglenden Befehlen kann ich die benötigten Beobachtungen aus dem gesamten Datensatz gewinnen.
 
 
Erzeugt ein dataset mit Hour Of Death + Cause Of Death + Number of Dead peaople in every hour 

```r
hod2 <- count(deaths, c("hod", "cod"))
```

```
## Error: object 'hod' not found
```

 
Enfernt Not a Number aus hod Spalte


```r
hod2 <- subset(hod2, !is.na(hod))  # Enfernt Not a Number aus hod Spalte
```

```
## Error: object 'hod2' not found
```


Da die Totesursachen mit Code angezeigt werden wollen wir nun unsere hod2 Dateien mit einer Tabelle die diese Codes erklärt


```r
codes <- read.csv("codes.csv")
```

```
## Warning: cannot open file 'codes.csv': No such file or directory
```

```
## Error: cannot open the connection
```


DAS HABE ICH EINFACH ABGESCHRIEBEN ADRIAN BITTE ERKLÄREN

```r
codes$disease <- sapply(codes$disease, function(x) str_c(strwrap(x, width = 30), 
    collapse = "\n"))
```

```
## Error: object 'codes' not found
```

```r
names(codes)[1] <- "cod"
```

```
## Error: object 'codes' not found
```

```r
codes <- codes[!duplicated(codes$cod), ]
```

```
## Error: object 'codes' not found
```




```r
hod2 <- join(hod2, codes, by = "cod")
```

```
## Error: object 'hod2' not found
```


Die ddply Funktion 


```r
hod2 <- ddply(hod2, "cod", transform, prop = freq/sum(freq))
```

```
## Error: object 'hod2' not found
```

```r
overall <- ddply(hod2, "hod", summarise, freq_all = sum(freq))
```

```
## Error: object 'hod2' not found
```

```r
overall <- transform(overall, prop_all = freq_all/sum(freq_all))
```

```
## Error: object 'overall' not found
```

```r
hod2 <- join(hod2, overall, by = "hod")
```

```
## Error: object 'hod2' not found
```

```r


devi <- ddply(hod2, "cod", summarise, n = sum(freq), dist = mean((prop - prop_all)^2))
```

```
## Error: object 'hod2' not found
```

```r
devi <- subset(devi, n > 50)
```

```
## Error: object 'devi' not found
```







You can also embed plots, for example:


```r
ggplot(data = devi, aes(x = n, y = dist)) + geom_point()
```

```
## Error: object 'devi' not found
```

```r
last_plot() + scale_x_log10() + scale_y_log10() + geom_smooth(method = "rlm", 
    se = F)
```

```
## Error: non-numeric argument to binary operator
```

```r
ggsave("n-dist-raw.pdf", width = 6, height = 6)
```

```
## Error: plot should be a ggplot2 plot
```


