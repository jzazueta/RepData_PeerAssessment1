Reproducible Research: Peer Assessment 1
======================================================================

### Loading and preprocessing the data

 
- Unzip "activity.zip" file--assumed to be on the working directory
read file
- gather complete cases and convert dates from strings into 
date objects:


```r
 file <- unzip("activity.zip")
        steps <- read.csv(file)
        steps <- steps[complete.cases(steps),]
        steps$date<-as.Date(steps$date)
```
 
#What is the mean total number of steps taken per day?
###Generate histogram of steps and calculate mean and median steps per day

- Aggregate steps by day
- Generate histogram
- Calculate **mean** and **median** values


```r
        daily.steps <-aggregate(steps~date,steps,sum)[,2]
        dates <-aggregate(steps~date,steps,sum)[,1]
        hist(daily.steps, main = "Total Steps per Day", xlab = "Total Steps", col="darkorange")
```

![plot of chunk unnamed-chunk-2](./PA1_template_files/figure-html/unnamed-chunk-2.png) 

```r
        mean(daily.steps)
```

```
## [1] 10766
```

```r
        median(daily.steps)
```

```
## [1] 10765
```

## What is the average daily activity pattern?

- Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)




```r
        daily.pattern<-aggregate(steps~interval,steps,mean)
        plot(daily.pattern$interval,daily.pattern$steps, type="l", main= "Daily Activity Pattern", xlab="5-minute activity interval", ylab="Average number of steps",col = "darkorange")
```

![plot of chunk unnamed-chunk-3](./PA1_template_files/figure-html/unnamed-chunk-3.png) 

- Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?


```r
        daily.pattern[daily.pattern$steps==max(daily.pattern$steps),]$interval
```

```
## [1] 835
```

## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
