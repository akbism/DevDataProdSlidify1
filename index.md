---
title       : "Developing Data Products Slidify"
subtitle    : "World Development Index Explorer"
author      : Amar Kumar
job         : Coursera Data Science Specialization - Developing Data Products
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Introduction

Project Idea: To create a tool to analyze the relationship and trend of any two world development indicators over period of time. 

1. Understand the world development indicators available in the world bank database. 
2. Select any two indicators of your choice for analysis.
3. Analyze/Download the data pertaining to the selected indicators realtime from the worldbank database.
4. Visualization of the data using animated dashboard.

The application allow the user to investigate the trends of the indicators over years in order to answer questions such as:

        How is the relationship between two indicators changing for all countries over period of time?

--- .class #id

## Obtaining Indicators Model Data

- The primary World Bank collection of development indicators presents the most current and accurate global development data available, and includes national, regional and global estimates.
- The application uses `WDI` [R package](https://github.com/vincentarelbundock/WDI) to fetch realtime data from the worldbank database.
- The extraction of data against the two selected indictors for all countries is demonstrated here. 
-The cleaning of data is also taken care of. 


```r
library(shiny);library(WDI);library(ISOcodes);library(googleVis);data(ISO_3166_1)
FUN<-function(x) {nation<-ISO_3166_1[,2] ;x<-subset(x,select=-c(iso2c, region, income, lending)); x<-x[x$iso3c %in% nation,];x[complete.cases(x),]}
ind<-c("AG.PRD.CROP.XD","AG.LND.AGRI.ZS") 
# Example- Crop production index (2004-2006 = 100) and Agricultural land (% of land area)
mydata<-FUN(WDI(indicator=c(ind[1],ind[2]),country = "all",  extra=T))
head(mydata,1)
```

```
##                 country year AG.PRD.CROP.XD AG.LND.AGRI.ZS iso3c   capital
## 43 United Arab Emirates 2006          90.64          6.502   ARE Abu Dhabi
##    longitude latitude
## 43   54.3705  24.4764
```

--- .class #id

## Visualization through animated Dashboard

- The application uses googleVis [R package] (http://github.com/mages/googleVis) to create motion chart and Geo chart. 


<iframe src="https://github.com/akbism/DevDataProdSlidify/blob/master/MergedID3640741f505f.html" frameborder="0", width="620", height="420">Loading</iframe>

--- .class #id

## Instructions for the WDI Explorer App

- The user has to select two appropriate indicators of his choice
- The application fetched the data table from the worldbank database on realtime basis.
- Further the user can analyze the relationship between the two indicators in the animated dashboard tab. 
- The result is 3 maps (e.g., map in previous slide) showing the geographical charts of the two indicators and motion chart to display relationship between the two indicators.
- All the three maps have play options in the app to display varrying situation over period of time.
- check it out at: https://akbism.shinyapps.io/WDI_EXPLORER/

