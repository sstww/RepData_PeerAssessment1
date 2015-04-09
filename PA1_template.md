# Reproducible Research: Peer Assessment 1

  
## Loading and preprocessing the data


```r
unzip("activity.zip")
act<-read.csv("activity.csv", header=TRUE, na.strings="NA")

library (lubridate) 
act$date<-ymd(act$date)
summary(act)
```

```
##      steps             date               interval     
##  Min.   :  0.00   Min.   :2012-10-01   Min.   :   0.0  
##  1st Qu.:  0.00   1st Qu.:2012-10-16   1st Qu.: 588.8  
##  Median :  0.00   Median :2012-10-31   Median :1177.5  
##  Mean   : 37.38   Mean   :2012-10-31   Mean   :1177.5  
##  3rd Qu.: 12.00   3rd Qu.:2012-11-15   3rd Qu.:1766.2  
##  Max.   :806.00   Max.   :2012-11-30   Max.   :2355.0  
##  NA's   :2304
```

## What is mean total number of steps taken per day?


```r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
## 
## The following objects are masked from 'package:lubridate':
## 
##     intersect, setdiff, union
## 
## The following object is masked from 'package:stats':
## 
##     filter
## 
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
act1<-act %>%
  group_by(date) %>%
  summarise(sum_steps=sum(steps, na.rm=TRUE))
mean_act1<-mean(act1$sum_steps, na.rm=TRUE)  
median_act1<-median(act1$sum_steps, na.rm=TRUE)  
hist(act1$sum_steps,
                main = "Histogram of Total Steps Taken by Day",
                xlab = "Total Steps per Day")
```

![](PA1_template_files/figure-html/unnamed-chunk-2-1.png) 

```r
mean_act1
```

```
## [1] 9354.23
```

```r
median_act1
```

```
## [1] 10395
```


## What is the average daily activity pattern?


```r
act2<-act %>%
  group_by(interval) %>%
  summarise(ave_interval_steps=mean(steps, na.rm=TRUE))

plot(act2$interval, act2$ave_interval_steps, type="l",
      main = "Aveage Steps by Interval for All Days",
      xlab="Intervals",
      ylab = "Average Steps" )
```

![](PA1_template_files/figure-html/unnamed-chunk-3-1.png) 

```r
max_steps<-act2[act2$ave_interval_steps==max(act2$ave_interval_steps), ]

max_steps
```

```
## Source: local data frame [1 x 2]
## 
##   interval ave_interval_steps
## 1      835           206.1698
```


## Imputing missing values

1.Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with NAs)

```r
total_missing<-length(is.na(act$steps))
total_missing
```

```
## [1] 17568
```

2.use the mean for that 5-minute interval to fill in all of the missing values in the dataset. 


```r
library(dplyr)
act3<-inner_join(act, act2)
```

```
## Joining by: "interval"
```

```r
act3$ave_interval_steps<-round(act3$ave_interval_steps, digits=0)
act3$ave_interval_steps<-as.integer(act3$ave_interval_steps)
act3$steps[is.na(act3$steps)==T] <- act3$ave_interval_steps[is.na(act3$steps)==T]
```

3.Create a new dataset that is equal to the original dataset but with the missing data filled in.


```r
act4<-act3[, (1:3)]
```

4.Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?


```r
library(dplyr)
act5<-act4 %>%
  group_by(date) %>%
  summarise(sum_steps=sum(steps, na.rm=TRUE))
mean_act5<-mean(act1$sum_steps, na.rm=TRUE)  
median_act5<-median(act1$sum_steps, na.rm=TRUE)  
hist(act5$sum_steps,
                main = "Histogram of Total Steps Taken by Day",
                xlab = "Total Steps per Day")
```

![](PA1_template_files/figure-html/unnamed-chunk-7-1.png) 

```r
mean_act5
```

```
## [1] 9354.23
```

```r
median_act5
```

```
## [1] 10395
```

## Are there differences in activity patterns between weekdays and weekends?

1.Create a new factor variable in the dataset with two levels - "weekday" and "weekend" indicating whether a given date is a weekday or weekend day.


```r
act6<-act4 %>%
  mutate(day=weekdays(date)) 

act6$weekdayend[act6$day=="Saturday"|act6$day=="Sunday"]<-"Weekend" 
act6$weekdayend[is.na(act6$weekdayend)==T]<-"Weekday" 
act6$weekdayend<-factor(act6$weekdayend)
```

2.Make a panel plot containing a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all weekday days or weekend days (y-axis). See the README file in the GitHub repository to see an example of what this plot should look like using simulated data.


```r
require(ggplot2)
```

```
## Loading required package: ggplot2
```

```r
ggplot(act6, aes(interval, steps))+
  geom_line()+
  facet_wrap(~weekdayend, nrow=2)+
  facet_wrap(~weekdayend, ncol=1)+
  xlab("Interval")+
  ylab("Number of steps")
```

![](PA1_template_files/figure-html/unnamed-chunk-9-1.png) 
