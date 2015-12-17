# Reproducible Research: Peer Assessment 1

Before beginning, we set the global options for the file.

```r
library('knitr')
# set global options for this document
opts_chunk$set(echo=TRUE, results="asis")
```

---

## Part I: Loading and preprocessing the data

Check for the `data` directory and create it if necessary.

```r
if (!file.exists("data")) {
  dir.create("data")
}
```
This directory is ignored by git, so that we don't commit both the zipped and unzipped data.


If the zipfile exists but hasn't been extracted, extract it.

```r
if (!file.exists("data/activity.csv")) {
  unzip("activity.zip", exdir="data", overwrite=FALSE)
}
```

Read in the data from the file.

```r
data <- read.csv("data/activity.csv")
```

---

## Part II: What is mean total number of steps taken per day?
> For this part of the assignment, you can ignore the missing values in the dataset.

### Make a histogram of the total number of steps taken each day

### Calculate and report the mean and median total number of steps taken per day

## What is the average daily activity pattern?



## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
