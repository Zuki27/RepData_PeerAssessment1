---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document:
    keep_md: true
---


## Loading and preprocessing the data


```r
dataset <- read.csv("activity.csv")
```


## What is mean total number of steps taken per day?


```r
steps <- aggregate(steps ~ date, dataset, sum)

hist(steps$steps, main = "Steps taken per day", xlab = "Number of steps", col = "purple", breaks = 8)
```

![](PA1_template_files/figure-html/unnamed-chunk-2-1.png)<!-- -->
## The mean and the median



```r
Mean <- mean(steps$steps)

print(Mean)
```

```
## [1] 10766.19
```

```r
Median <- median(steps$steps)

print(Median)
```

```
## [1] 10765
```


## What is the average daily activity pattern?


```r
DailyActivity <- aggregate(steps ~ interval, dataset, mean)
plot(DailyActivity$interval, DailyActivity$steps, type = "l", xlab = "5 minute interval", ylab = "Average of all days", main =  "Average daily activity", col = "red")
```

![](PA1_template_files/figure-html/unnamed-chunk-4-1.png)<!-- -->



```r
DailyActivity$interval[which.max(DailyActivity$steps)]
```

```
## [1] 835
```


## Imputing missing values


```r
nrow(dataset[is.na(dataset$steps),])
```

```
## [1] 2304
```


```r
NoNA <- dataset

NoNA[is.na(NoNA$steps), "steps"] <- 0


day <- aggregate(steps ~ date, NoNA, sum)
hist(day$steps, main = "Number of steps per day", xlab = "Steps", col = "green", breaks = 8)
```

![](PA1_template_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

## Are there differences in activity patterns between weekdays and weekends?
