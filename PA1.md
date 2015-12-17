# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data

Check for the `data` directory and create it if necessary.  This directory is ignored by git, so that we don't commit both the zipped and unzipped data.

```r
if (!file.exists("data")) {
  dir.create("data")
}
```

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


## What is mean total number of steps taken per day?



## What is the average daily activity pattern?



## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
