# Reproducible Research: Peer Assessment 1

Before beginning, we set the global options for the file.

```r
library('knitr')
library('ggplot2')

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

To prepare the histogram, we first need to aggregate the steps by date.


```r
daily_steps <- aggregate(steps ~ date, data = data, sum)
```

Note that aggregate throws out the days for which there is `NA` data - there are 61 unique days in the dataset, but only 53 of them have steps logged.

Then we can produce the histogram.  Setting the bin width to 500 gives a clearer picture of the distribution.


```r
ggplot(data = daily_steps, aes(daily_steps$steps)) +
      geom_histogram(binwidth = 500) +
      ggtitle('Days with Step Count') +
      xlab('Steps') +
      ylab('Days')
```

![](PA1_files/figure-html/steps_per_day_histogram-1.png) 


### Calculate and report the mean and median total number of steps taken per day

Using the aggreated data, we can calculate the mean (rounded to two decimal places)


```r
steps_mean <- format(mean(daily_steps$steps), nsmall=2)
```

and the median


```r
steps_median <- median(daily_steps$steps)
```

and report the figures.

The mean daily step count is __10766.19__ steps per day, and the median daily step count is __10765__ steps per day.



---

## What is the average daily activity pattern?

### Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)

To produce the time series plot, we first need to aggregate the data by interval.


```r
interval_mean <- aggregate(steps ~ interval, data = data, mean)
```

Then plot it as a line


```r
ggplot(data = interval_mean, aes(y = interval_mean$steps,
                                 x = interval_mean$interval)
       ) +
      geom_line() +
      ggtitle('Mean Daily Steps/Interval') +
      xlab('Interval') +
      ylab('Mean Steps')
```

![](PA1_files/figure-html/interval_mean_line-1.png) 

### Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?

We can identify the maximum interval and see that it matches with the observations from the graph


```r
max_interval <- interval_mean[interval_mean$steps == max(interval_mean$steps), ]
```

The maximum 5-minute interval is number __835__, with an average step count of __206.1698113__.



---

## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
