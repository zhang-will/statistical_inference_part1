---
title: "statistical_inference_course_project_1"
output: html_document
---

This project investigates the exponential distribution in R and compare it with the Central Limit Theorem. The exponential distribution can be simulated in R with rexp(n, lambda) where lambda is the rate parameter. The mean of exponential distribution is 1/lambda and the standard deviation is also 1/lambda. Set lambda = 0.2 for all of the simulations. You will investigate the distribution of averages of 40 exponentials.


```r
Lambda = 0.2
n = 40
nSims = 1:1000
set.seed(820)
Means <- data.frame(x = sapply(nSims, function(x) {
    mean(rexp(n, Lambda))
}))
head(Means)
```

```
##          x
## 1 5.750000
## 2 3.808205
## 3 4.058154
## 4 3.999241
## 5 4.312532
## 6 4.418246
```


```r
m = mean(Means$x)
m
```

```
## [1] 4.998812
```


```r
sd = sd(Means$x)
sd
```

```
## [1] 0.7909422
```

Expected standard deviation


```r
(1/Lambda)/sqrt(40)
```

```
## [1] 0.7905694
```

Variance of simulations


```r
var(Means$x)
```

```
## [1] 0.6255895
```

Expected Variance


```r
((1/Lambda)/sqrt(40))^2
```

```
## [1] 0.625
```

1.The expected center (5.0) is very close to the center of the distribution (4.9988).
The standard deviation (0.7909) is also close to the expected standard deviation (0.79056). 

To show that the distribution is approximately normal


```r
library(ggplot2)
ggplot(data = Means, aes(x = x)) + geom_histogram(aes(y = ..density..), fill = I("darkolivegreen3"), 
    binwidth = 0.2, color = I("black")) + stat_function(fun = dnorm, arg = list(mean = 5, 
    sd = sd(Means$x)))
```

![plot of chunk unnamed-chunk-7](figure/unnamed-chunk-7-1.png) 

3. The histogram plot depicts a distribution that is approximately normal (mean = 5; sd = .7909). 

To evaluate the coverage of the confidence interval for 1/lambda: X¯±1.96Sn???)


```r
mean(Means$x) + c(-1, 1) * 1.96 * sd(Means$x)/sqrt(nrow(Means))
```

```
## [1] 4.949789 5.047835
```

4. The 95% confidence interval for the mean of the means is 4.950 - 5.047.
