---
title: "Advanced Bioinformatics 2019 Assessment"
author: "9534"
date: "05/06/2019"
output: 
  html_document: 
    keep_md: yes
keep_md: yes
---

# TASK 1

```r
sum(5:55)
```

```
## [1] 1530
```

# TASK 2

```r
sumfun<- function (n) 
sum(5:n)
```

sumfun(10)

```r
sum(5:10)
```

```
## [1] 45
```
sumfun(20)

```r
sum(5:20)
```

```
## [1] 200
```
sumfun(100)

```r
sum(5:100)
```

```
## [1] 5040
```
# TASK 3

```r
Fibonacci_seq <- numeric(12)
Fibonacci_seq[1] <- 1
Fibonacci_seq[2] <- 1
for (i in 3:12) { 
   Fibonacci_seq[i] <- Fibonacci_seq[i-1]+Fibonacci_seq[i-2]
}
print("The first 12 numbers of the Fibonacci sequence are:")
```

```
## [1] "The first 12 numbers of the Fibonacci sequence are:"
```

```r
print(Fibonacci_seq)
```

```
##  [1]   1   1   2   3   5   8  13  21  34  55  89 144
```
# TASK 4

```r
library(ggplot2)
ggplot(data=mtcars,aes(x=as.factor(gear),y=mpg,fill=gear)) + geom_boxplot()
```

![](Advanced_Bioinformatics_2019_Assessment_FINAL_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

# TASK 5


```r
cars.lm <- lm(dist ~ speed, data = cars)
summary(cars.lm)
```

```
## 
## Call:
## lm(formula = dist ~ speed, data = cars)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -29.069  -9.525  -2.272   9.215  43.201 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept) -17.5791     6.7584  -2.601   0.0123 *  
## speed         3.9324     0.4155   9.464 1.49e-12 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 15.38 on 48 degrees of freedom
## Multiple R-squared:  0.6511,	Adjusted R-squared:  0.6438 
## F-statistic: 89.57 on 1 and 48 DF,  p-value: 1.49e-12
```
Intercept: -17.5791 
Fitted Slope: 3.9324
Standard Deviation Speed: 0.4155
Standard Deviation Distance: 6.7584

# TASK 6

```r
library(grid)
library(gridExtra)
library(gtable)
lm.scatter <- ggplot(cars, aes(x=speed, y=dist)) + 
  geom_point(color='#2980B9', size = 4) + xlim(c(0, 25)) + 
  geom_smooth(method=lm, se=FALSE, fullrange=TRUE, color='#2C3E50') + 
  labs(title='Linear relationship Between Speed and Breaking Distance')
grid.arrange(lm.scatter)
```

![](Advanced_Bioinformatics_2019_Assessment_FINAL_files/figure-html/unnamed-chunk-9-1.png)<!-- -->

# TASK 7


```r
new_speed <- cars$speed * (5280/3600)
line<-lm(dist ~ 0+ new_speed + I(new_speed^2),cars)
summary(line)
```

```
## 
## Call:
## lm(formula = dist ~ 0 + new_speed + I(new_speed^2), data = cars)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -28.836  -9.071  -3.152   4.570  44.986 
## 
## Coefficients:
##                Estimate Std. Error t value Pr(>|t|)   
## new_speed       0.84479    0.38180   2.213  0.03171 * 
## I(new_speed^2)  0.04190    0.01366   3.067  0.00355 **
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 15.02 on 48 degrees of freedom
## Multiple R-squared:  0.9133,	Adjusted R-squared:  0.9097 
## F-statistic: 252.8 on 2 and 48 DF,  p-value: < 2.2e-16
```

```r
library(ggplot2)
y <- cars$dist
x <- cars$new_speed
ggplot(cars,aes(new_speed,dist)) + 
    geom_point(color='Black', size = 1) + xlim(c(0,40)) +
 geom_smooth(method = "lm", formula = "y ~ 0 + x + I(x^2)",  color="red", fullrange='TRUE') + labs(title= 'Reaction Time for Driver to Start Breaking ', y = 'Stopping Distance (feet)', x = "Speed")
```

![](Advanced_Bioinformatics_2019_Assessment_FINAL_files/figure-html/unnamed-chunk-11-1.png)<!-- -->

Yes the result 0.84479 is a reasonable reaction speed.
