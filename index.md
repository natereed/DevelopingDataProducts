---
title       : Prediction Function for Iris Data
subtitle    : 
author      : Nate Reed
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Overview

We used the Iris data set and built a predictive model. An accurate prediction of flower species was developed using only the following attributes:

- Sepal Length
- Sepal Width
- Petal Width
- Petal Length

--- .class #id 

## Plots

Shown here are plots relating pairs of sepal and petal attributes with species:

![plot of chunk unnamed-chunk-1](assets/fig/unnamed-chunk-1-1.png) 

---

## Methodology

Random Forest, a highly accurate classification and regression algorithm, was used for the predictive model. The procedure was as follows:

1. Data was partitioned into training and test sets:
2. Random forest was applied to the training set to build the model. 
3. Random forest was applied to the test set to verify accuracy.

---

## Partitioning


```r
library(caret)
library(randomForest)
library(e1071)
data(iris)
set.seed(12345)
inTrain<-createDataPartition(iris$Species, p=0.7, list=FALSE)
training<-iris[inTrain,]
testing<-iris[-inTrain,]
```

---

## Modeling

First, the model was trained:


```r
modfit<-train(Species~., method="rf", data=training)
```

Model fit was assessed on the testing set. As we see below, there was only one inaccurate classification out of 45:


```r
predictions<-predict(modfit, testing[,-5])
table(predictions, testing$Species)
```

```
##             
## predictions  setosa versicolor virginica
##   setosa         15          0         0
##   versicolor      0         15         1
##   virginica       0          0        14
```

