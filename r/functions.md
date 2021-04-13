# Important r-functions

- [Important r-functions](#important-r-functions)
  - [Important parameters:](#important-parameters)
  - [Normal distribution](#normal-distribution)
    - [dnorm(x, mean = 0, sd = 0)](#dnormx-mean--0-sd--0)
    - [pnorm(q, mean = 0, sd = 0, lower.tail = TRUE)](#pnormq-mean--0-sd--0-lowertail--true)
    - [qnorm(p, mean = 0, sd = 0, lower.tail = TRUE)](#qnormp-mean--0-sd--0-lowertail--true)
    - [rnorm(n, mean = 0, sd = 1)](#rnormn-mean--0-sd--1)
  - [Binomial distribution](#binomial-distribution)
    - [dbinom(x, size, prob)](#dbinomx-size-prob)
    - [pbinom(q, size, prob, lower.tail = TRUE)](#pbinomq-size-prob-lowertail--true)
    - [qbinom(p, size, prob, lower.tail = TRUE)](#qbinomp-size-prob-lowertail--true)
    - [rbinom(n, size, prob)](#rbinomn-size-prob)
  - [Uniform distribution](#uniform-distribution)
    - [dunif(x, min = 0, max = 1, log = FALSE)](#dunifx-min--0-max--1-log--false)
    - [punif(q, min = 0, max = 1, lower.tail = TRUE, log.p = FALSE)](#punifq-min--0-max--1-lowertail--true-logp--false)
    - [qunif(p, min = 0, max = 1, lower.tail = TRUE, log.p = FALSE)](#qunifp-min--0-max--1-lowertail--true-logp--false)
    - [runif(n, min = 0, max = 1)](#runifn-min--0-max--1)
  - [Poisson distribution](#poisson-distribution)
    - [dpois(x, lambda)](#dpoisx-lambda)
    - [ppois(q, lambda, lower.tail = TRUE)](#ppoisq-lambda-lowertail--true)
    - [qpois(p, lambda, lower.tail = TRUE)](#qpoisp-lambda-lowertail--true)
    - [rpois(n, lambda)](#rpoisn-lambda)
  - [Students t-distribution](#students-t-distribution)
    - [dt(x, df)](#dtx-df)
    - [pt(q, df, lower.tail = TRUE)](#ptq-df-lowertail--true)
    - [qt(p, df, lower.tail = TRUE)](#qtp-df-lowertail--true)
    - [rt(n, df)](#rtn-df)
  - [f-distribution](#f-distribution)
    - [df(x, df1, df2)](#dfx-df1-df2)
    - [pf(q, df1, df2, lower.tail = TRUE)](#pfq-df1-df2-lowertail--true)
    - [qf(p, df1, df2, lower.tail = TRUE)](#qfp-df1-df2-lowertail--true)
    - [rf(n, df)](#rfn-df)
  - [t-Test](#t-test)
    - [One-Sample](#one-sample)
    - [Two-Sample](#two-sample)
  - [ANOVA](#anova)
  - [Regression](#regression)
    - [Regression line](#regression-line)
    - [Regression output](#regression-output)
  - [Proportions](#proportions)
    - [One sample](#one-sample-1)
    - [Two sample](#two-sample-1)
  - [Other](#other)
    - [median(x)](#medianx)
    - [quantile(x, percentile)](#quantilex-percentile)
    - [sample(x, n)](#samplex-n)
    - [mean(x)](#meanx)
    - [sd(x)](#sdx)
    - [seq(from = 1, to = 1, by = ((to - from)/(length.out - 1))](#seqfrom--1-to--1-by--to---fromlengthout---1)
    - [length(x)](#lengthx)
    - [choose(n, k)](#choosen-k)
    - [sum(x)](#sumx)
    - [hist(x)](#histx)
    - [stripchart(x)](#stripchartx)
  - [Sources](#sources)

Functions that start with:
- `d` return the **Probability Mass Function** (PMF) for discrete distributions and the **Probability Density Function** (PDF) for continuos distributions
- `p` return the **Cumulative Density Function** (CDF).
- `q` return the value at a given quantile.
  - 99.5

## Important parameters:
- **lower.tail**: Specifies which range is calculated. Either the range below a value is calculated or the range above value. Specifies which area is calculated. 
  - `lower.tail = TRUE` (default): 
    - P(X <= x) is calculated  
  - `lower.tail = FALSE`:
    - P(X > x) is calculated

## Normal distribution

- **mean**: Mean
- **sd**: Standard deviation

### dnorm(x, mean = 0, sd = 0)

`x` is the value for which I want the probability. In the example below, I calculate the probability for the value 0.

```r
mean <- 0
sd <- 1

# Gives me the probability of EXACTLY 0 given a standard normal distribution.
dnorm(0, mean, sd)
> [1] 0.3989
```

### pnorm(q, mean = 0, sd = 0, lower.tail = TRUE)

`q` is the value up to which we want to calculate the probability. So we calculate the probability for q or less **P(X <= q)**. If you set `lower.tail = FALSE`, then you calculate the upper part. So **P(X > q)** is calculated or also **1 - P(X <= q)**.

*lower.tail = TRUE*:
```r
mean <- 170
sd <- 25

# Gives me the probability of having size 170 or less (-infty, 170). 
# Since the value corresponds to the Mean this value lies exactly in the middle, why 50% comes out. 
# Since 50% of the distribution lies to the left of this value.
pnorm(170, mean, sd)
> [1] 0.5
```
*lower.tail = FALSE*:
```r
mean <- 170
sd <- 25

# Gives me the probability of being greater than 170 (X > 170). 
# Since the value corresponds to the mean, this value lies exactly in the middle, which is why 50% comes out. 
# Since 50% of the distribution lies to the right of this value.
pnorm(170, mean, sd, lower.tail=FALSE)
> [1] 0.5
```

```r
mean <- 170
sd <- 25

# Gives me the probability of being between 150cm and 170cm tall
pnorm(170, mean, sd) - pnorm(150, mean, sd)
> [1] 0.2881446
```

This calculation is equivalent to when something is read out of the normal distribution tables.

**IQR (Inner Quartile Range)**:

- Value at 75% of the distribution - Value at 25% of the distribution
- (75% - 25%)
- ```qnorm(0.75, mean, sd) - qnorm(0.25, mean, sd)```


### qnorm(p, mean = 0, sd = 0, lower.tail = TRUE)

p is the value of a percentile at which I want to calculate the value. For example, if I want to calculate how tall 50% of the people are: 

*lower.tail = TRUE*:
``` r
mean <- 170
sd <- 25

# Gives me the value where 50% of the distribution is over. 
# In a height distribution, this would be 170, since this value is the mean and lies exactly in the middle.
# That is 50% of the people are <= 170cm
qnorm(0.5, mean, sd)
> [1] 170
```
This gives me the value when I look at the distribution from the left.

If I work with `lower.tail = FALSE`, then I start looking at the distribution from the right. 
*lower.tail = FALSE*:
``` r
mean <- 170
sd <- 25

# Gives me the value where 60% of the distribution is over. 
# With a height distribution this would be 176.3337. That is 60% of the people are <= 170cm
qnorm(0.6, mean, sd, lower.tail=TRUE)
> [1] 176.3337

# We look at the distribution from the right look where 60% of the distribution is over. 
# This result would be equal to the calculation of I look from the left 40%.
qnorm(0.6, mean, sd, lower.tail=FALSE)
> [1] 163.6663

# The same result as in the example above, because we look from the left 40% away. 
# Above we looked from the right 60% away, which is the same as the 40% from the left.
qnorm(0.4, mean, sd)
> [1] 163.6663
```

This calculation would be to read out the tables of the standard normal distributions upside down. So read out the value from the percentages.

### rnorm(n, mean = 0, sd = 1)

This function takes `n` samples from the given normal distribution. Below we take 5 samples from a normal distribution with a **mean** of 170 and a **standard deviation** of 25.

```r
mean <- 170
sd <- 25

# Takes 5 samples from the given normal distribution.
rnorm(5, mean, sd)
> [1] 142.5524 137.7176 191.2217 182.7569 153.9343

# Different values for every time we execute this.
rnorm(5, mean, sd)
> [1] 171.9180 181.8101 140.1300 188.3176 181.7031
```

## Binomial distribution

- **x**: Number of successful attempts for which we are looking for the probability
- **size**: Number of successful attempts for which we are looking for the probability
- **prob**: Probability for a successful attempt

### dbinom(x, size, prob)

x is the number of successful trials for which we are looking for the probability. I use this function to calculate the value of a PMF at location x. In the example below, I calculate the probability of getting exactly 5 heads in 10 coin tosses.

```r
n <- 10
prob <- 1/2

# Probability to get exactly 5 heads in 10 throws with a probability of 50%.
dbinom(5, n, prob)
> [1] 0.2460938
```
### pbinom(q, size, prob, lower.tail = TRUE)

`q` is the value up to which we want to calculate the probability. So we calculate the probability for q or less **P(X <= q)**. If you set `lower.tail = FALSE`, then you calculate the upper part. So **P(X > q)** is calculated or also **1 - P(X <= q)**.

*lower.tail = TRUE*:
```r
n <- 10
prob <- 1/2

# Gives me the probability of throwing 5 or less heads.
pbinom(5, n, prob)
> [1] 0.6230469
```
*lower.tail = FALSE*:
```r
n <- 10
prob <- 1/2

# Gives me the probability of throwing more than 5 heads. 
# Is exactly the opposite probability to the example above.
pbinom(5, n, prob)
> [1] 0.3769531
```

### qbinom(p, size, prob, lower.tail = TRUE)

p is the value of a percentile at which I want to calculate the value. If I want to calculate how many heads I get with 60% probability.

*lower.tail = TRUE*:
``` r
n <- 10
prob <- 1/2

# Gives me the number of heads that occur with 50% probability. 
# 5 heads occur with a probability of 50%.
qbinom(0.5, 10, 0.5)
> [1] 5
```

### rbinom(n, size, prob)

This takes `n` samples from the given binomial distribution. Below we take 5 samples from a binomial distribution. In the example below a coin is thrown 10 for 5 rounds. And the number of heads in each of the 5 rounds are in the result.

``` r
n <- 10
prob <- 1/2

# A coin is thrown 10 times and 
rbinom(5, 10, 0.5)
> [1] 7 6 6 5 6
```

## Uniform distribution

- **x**: Value in the interval, which I am looking for
- **min**: Start value of the interval
- **max**: End value of the interval

### dunif(x, min = 0, max = 1, log = FALSE)
`x` is the value for which I want the probability. The example below is about an interval of 60 minutes. I calculate the probability that the train will arrive in the 3 minute. The area of the uniform distribution is exactly 1 and a rectangle. Therefore, the probability of the train coming in a given minute is always the same, no matter what. Summing up the probability then gives 1.

```r
min <- 0
max <- 60

# Gives me the probability that the train will arrive exactly in the third minute. 
# The probability is the same for each minute.
dunif(3, min, max)
> [1] 0.01666667
```
### punif(q, min = 0, max = 1, lower.tail = TRUE, log.p = FALSE)

`q` is the value up to which we want to calculate the probability. So we calculate the probability for q or less **P(X <= q)**. If you set `lower.tail = FALSE`, then you calculate the upper part. So **P(X > q)** is calculated or also **1 - P(X <= q)**.

*lower.tail = TRUE*:
```r
min <- 0
max <- 60

# Gives me the probability that the train will arrive in the first 20 minutes. 
# To do this, simply calculate the probability for 1 minute * 20.
punif(20, min, max)
> [1] 0.3333333
```
*lower.tail = FALSE*:
```r
min <- 0
max <- 60

# Gives me the probability that the train will arrive in the last 20 minutes. 
# Here is looked from the value 40 to the right in the distribution.
punif(40, min, max, lower.tail=FALSE)
> [1] 0.3333333
```

### qunif(p, min = 0, max = 1, lower.tail = TRUE, log.p = FALSE)

p is the value of a percentile at which I want to calculate the value. Here 50% would give 30 minutes, because after 50% of the distribution 30 minutes have passed.

*lower.tail = TRUE*:
``` r
min <- 0
max <- 60

# Gives me the value where 50% of the distribution is over. 
# For one hour, that would be 30 minutes
qunif(0.5, min, max)
> [1] 170
```
This gives me the value when I start looking at the distribution from the left.

If I work with `lower.tail = FALSE`, then I start to look at the distribution from the right.
*lower.tail = FALSE*:
``` r
min <- 0
max <- 60

# Gives me the value where 60% of the distribution is over. 
qunif(0.6, min, max, lower.tail=TRUE)
> [1] 36

# We look at the distribution from the right look where 60% of the distribution is over. 
# This result would be equal to the calculation of I look from the left 40%. 
# Both values must balance out to 60 in total, because that's how big the interval is
qunif(0.6, min, max, lower.tail=FALSE)
> [1] 24

# The same result as in the example above, because we look from the left 40% away. 
# Above we looked from the right 60% away, which is the same as the 40% from the left.
qnorm(0.4, min, min)
> [1] 24
```

### runif(n, min = 0, max = 1)

This function takes `n` samples from the given uniform distribution. Below we take 5 samples from a uniform distribution with a **min** of 0 and a **max** of 1.

```r
min <- 0
max <- 60

# Takes 5 samples from the given normal distribution.
runif(5, min, max)
> [1] 27.61924 57.08847  2.01578 48.82894 48.65880

# Different values for every time we execute this.
runif(5, min, max)
> [1] 34.69196 49.87289 23.74119 22.55579 48.04149
```

## Poisson distribution

- **lambda**: How often the event occurs in a time interval?

### dpois(x, lambda)
`x` is the value for which I want the probability. In the example below, I calculate the probability that 1 hurricane occurs in a year.

```r
years <- 22
hurricans <- 27

lambda <- hurricans/years # 1.227 hurricans per year

# Gives me the probability that EXACTLY 1 hurricane will occur
dpois(1, lambda)
> [1] 0.3597024
```
### ppois(q, lambda, lower.tail = TRUE)

`q` is the value up to which we want to calculate the probability. So we calculate the probability for q or less **P(X <= q)**. If you set `lower.tail = FALSE`, then you calculate the upper part. So **P(X > q)** is calculated or also **1 - P(X <= q)**.

*lower.tail = TRUE*:
```r
years <- 22
hurricans <- 27

lambda <- hurricans/years # 1.227 hurricans per year

# Gives me the probability of fewer than 3 hurricanes in a year.
ppois(2, lambda)
> [1] 0.8735197
```
*lower.tail = FALSE*:
```r
years <- 22
hurricans <- 27

lambda <- hurricans/years # 1.227 hurricans per year

# Gives me the probability that more than 2 hurricanes will occur in a year. 
# This is, of course, exactly the opposite probability to less than 3 hurricanes occurring.
ppois(2, lambda, FALSE)
> [1] 0.1264803
```

### qpois(p, lambda, lower.tail = TRUE)

p is the value of a percentile at which I want to calculate the value. For example, if I want to calculate how many hurricanes occur with 99.5% probability.

*lower.tail = TRUE*:
``` r
years <- 22
hurricans <- 27

lambda <- hurricans/years # 1.227 hurricans per year

# Gives me the number of hurricanes that occur with 99.5% probability in a year. 
# 5 or less hurricanes occur with a probability of 99.5% in a year
qpois(0.995, e)
> [1] 5
```

### rpois(n, lambda)

This function takes `n` samples from the given poisson distribution. Below we take 5 samples from a poisson distribution with lambda 27/22.

``` r
years <- 22
hurricans <- 27

lambda <- hurricans/years # 1.227 hurricans per year

# Returns 5 samples of how many hurricans can occur in one year.
rpois(5, lambda)
> [1] 0 4 2 2 2
```

## Students t-distribution

- **df**: Degrees of freedom, usually n-1

### dt(x, df)

`x` is the value for which I want the probability. In addition, I need the degrees of freedom in the example below. These are usually calculated from the sample size - 1. In the example below, I calculate the probability that 0 comes out as the value.

```r
mean <- 0
sd <- 1

# Gives me the probability that EXACTLY 0 comes out in a t-distribution.
dt(0, 10)
> [1] 0.3891084

dt(0, 200)
> [1] 0.3984439

dnorm(0)
> [1] 0.3989423

# As you can see, the t-distribution approaches the normal distribution the higher the sample size is.
```

### pt(q, df, lower.tail = TRUE)

`q` is the value up to which we want to calculate the probability. So one calculates the probability for q or less **P(X <= q)**. If you set `lower.tail = FALSE`, then you calculate the upper part. So **P(X > q)** is calculated or also **1 - P(X <= q)**.

*lower.tail = TRUE*:
```r
# Gives me the probability of having the value 1 or less in the standard normal distribution.
pnorm(1)
> [1] 0.8413447

# Gives me the probability of having the value 1 or less. 
# Here the 10 degrees of freedom are to be considered. 
# As you can see, the value is already very close to the value of the standard normal distribution.
pt(1, 10)
> [1] 0.8295534

# Same calculation as above, but with 200 degrees of freedom. 
# Value is significantly closer to the value of the standard normal distribution.
pt(1, 200)
> [1] 0.8407406
```

*lower.tail = FALSE*:
```r
# Gives me the probability of having more than the value 1. 
# This is exactly the opposite probability to above.
pt(1, 10, lower.tail=FALSE)
> [1] 0.1592594

pt(1, 200, lower.tail = FALSE)
> [1] 0.1592594
```

### qt(p, df, lower.tail = TRUE)

p is the value of a percentile at which I want to calculate the value. 

*lower.tail = TRUE*:
``` r

# Gives me the value where 60% of the distribution is over. 
qnorm(0.6)
> [1] 0.2533471

# Gives me the value where 60% of the distribution is over. 
# Note the 10 degrees of freedom. Value is already very close to that of the standard normal distribution
qt(0.6, 10)
> [1] 0.2601848

# Gives me the value where 60% of the distribution is over. 
# Note the 200 degrees of freedom.
# Value is even closer to the standard normal distribution.
qt(0.6, 200)
> [1] 0.2536844
```
This gives me the value when I start looking at the distribution from the left.

If I work with `lower.tail = FALSE`, then I start looking at the distribution from the right. So from the right away where 60% of the distribution is over.
*lower.tail = FALSE*:
``` r
# Gives me the value where 60% of the distribution is over. 
qt(0.6, 200, lower.tail=TRUE)
> [1] 0.2536844

# We look at the distribution from the right where 60% of the distribution is over. 
# This result would be equal to the calculation if I look from the left 40%.
qt(0.6, 200, lower.tail=FALSE)
> [1] -0.2536844

# The same result as in the example above, because we look from the left 40% away. 
# Above we looked from the right 60% away, which is the same as the 40% from the left.
qt(0.4, 200)
> [1] -0.2536844
```

### rt(n, df)

This function takes `n` samples from the given t-distribution. Below we take 5 samples from a t-distribution with 5 degrees of freedom.

``` r
rt(5, 20)
> [1] -0.56443901  0.09673789  0.21494985 -0.56269903 -1.63759219
```

## f-distribution

- **df1, df2**: degrees of freedom

### df(x, df1, df2)

`x` is the value for which I want the probability. In addition, I need the degrees of freedom in the lower example. In the lower example, I calculate the probability that 0 comes out as the value

```r
# Gives me the probability that EXACTLY 1 comes out in an f-distribution
df(1, 10, 10)
> [1] 0.6152344
```

### pf(q, df1, df2, lower.tail = TRUE)

`q` is the value up to which we want to calculate the probability. So we calculate the probability for q or less **P(X <= q)**. If you set `lower.tail = FALSE`, then you calculate the upper part. So **P(X > q)** is calculated or also **1 - P(X <= q)**.

*lower.tail = TRUE*:
```r
# Gives me the probability of having the value 2 or less. 
# Here the 10 degrees of freedom are to be considered. 
pf(1, 10, 10)
> [1] 0.8551542
```

*lower.tail = FALSE*:
```r
# Gives me the probability of having more than the value 2. 
# This is exactly the opposite probability to above.
pt(2, 10, lower.tail=FALSE)
> [1] 0.1448458
```

### qf(p, df1, df2, lower.tail = TRUE)

p is the value of a percentile at which I want to calculate the value. 

*lower.tail = TRUE*:
``` r
# Gives me the value where 60% of the distribution is over. 
# Note the 10 degrees of freedom.
qf(0.6, 10, 10)
> [1] 1.178651

```
This gives me the value when I start looking at the distribution from the left. So from the left, where are 60% of the distribution over.

### rf(n, df)

This function takes `n` samples from the given f-distribution. Below we take 5 samples from a f-distribution with 10 degrees of freedom.

``` r
rf(5, 10, 10)
[1] 3.1506333 1.4209381 3.4736313 0.3532966 1.3175930
```

## t-Test

### One-Sample

`t.test(x, y = NULL, alternative = c("two.sided", "less", "greater"), mu = 0, paired = FALSE, var.equal = FALSE, conf.level = 0.95, ...)`

We do a t-test like this. We have to pass the data specify the alternative hypothesis, give the population mean and specify the confidence level. In this example a two sided t-test with a significance of 5% is done.
```r
t.test(distanz, alternative = "two.sided", mu = meanDistance, conf.level = 0.95)
```

Below we see the results of the t-test above.
We see the value of the t-statistic `t = 1.4817` with the degrees of freedom `df=49` and the p-value for the t-statistic `p-value=0.1448`. We see the $H_1$ and the confidence interval for the `mean` and the `mean` itself. From the p-value we can decide if the $H_0$ is going to be rejected.
```r
	One Sample t-test

data:  distanz
t = 1.4817, df = 49, p-value = 0.1448
alternative hypothesis: true mean is not equal to 550
95 percent confidence interval:
 535.3142 647.1258
sample estimates:
mean of x 
   591.22 
```

### Two-Sample

```r
t.test(data1, data2, conf.level = 0.95)
```
Output:
```r
	Welch Two Sample t-test

data:  first and second
t = 1.539, df = 18.107, p-value = 0.1411
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
 -0.2486748  1.6130869
sample estimates:
 mean of x  mean of y 
-0.3913627 -1.0735688 
```

## ANOVA

```r
gr <- factor(rep(1:k, ni))
anova(aov(x ~ gr))
```

Output:
```r
Analysis of Variance Table

Response: x
          Df  Sum Sq Mean Sq F value    Pr(>F)    
gr         4  760.98  190.245  5.7623 0.0004425 ***
Residuals 72 2377.12  33.016                      
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
```

`gr` and `Sum Sq` is the **SSB** (760.98) in the formula. `Residuals` and `Sum Sq` is the **SSW** (2377.12) in the formula. 
`gr` and `Mean Sq` is the **MSB** (190.245) in the formula. `Residuals` and `Mean Sq` is the **MSW** (33.016) in the formula. 

## Regression

### Regression line
`lm(formula)` is used to fit linear models. It can be used to carry out regression, single stratum analysis of variance and analysis of covariance.

x: values on the x-axis
y: values on the y-axis

```r
lm(y ~ x)
```
Output:
```r
Call:
lm(formula = y ~ x)

Coefficients:
(Intercept)            x  
    42.9352       0.2324  
```

As you can see above the value for the *intercept* and the value of *slope* is calculated.

### Regression output

This gives us the outcome of the summary, but just the coefficient part.
```r
summary(lm(y~x))[["coefficients"]]
```
Output:
```r
              Estimate  Std. Error  t value    Pr(>|t|)
(Intercept) 42.9352244 10.47420105 4.099141 0.000439672
x            0.2323655  0.08110709 2.864922 0.008755851
```

As you can see `Estimate` and `x` is the slope of the regression line (0.2323655). 
`Std. Error` and `x` is the standard error $SE_b$ of the slope $\beta_1$ (0.08110709).
`t value` and `x` is the value of the t-statistic (2.864922).
`Pr(>|t|)` and `x` is the p-value of the t-statistic.

## Proportions

### One sample
```r
prop.test(x = 17, n = 58, conf.level=0.05)
```
**x**: success amount
**n**: total amount

Output:
```r
	1-sample proportions test with continuity
	correction

data:  17 out of 58, null probability 0.5
X-squared = 9.1207, df = 1, p-value = 0.002527
alternative hypothesis: true p is not equal to 0.5
95 percent confidence interval:
 0.1846295 0.4291019
```

In the output there is the p-value with the confidence interval.

### Two sample

In this example two frequencies are compared.
There are 110 students that have taken the lecture and 88 students that missed the lecture. From the 110 students 80 passed the lecture and from the 88 students 47 passed the lecture. We want to test, if taking the lecture has a positive effect on passing the lecture.

This is easily done in R with `prop.test`, where we pass to `x` a vector of the amount of students that passed the lecture separated by lecture taken and lecture missed.

As `n` we pass a vector with the total amount of students that have taken or missed the lecture.

```r
lectureTakenPassed <- 80
lectureMissedPassed <- 47
totalLectureTaken <- 110
totalLectureMissed <- 88

prop.test(
  x = c(lectureTakenPassed, lectureMissedPassed), 
  n = c(totalLectureTaken, totalLectureMissed)
)
```
Output:
```r
	2-sample test for equality of proportions with continuity correction

data:  c(lectureTakenPassed, lectureMissedPassed) out of c(totalLectureTaken, totalLectureMissed)
X-squared = 7.1148, df = 1, p-value = 0.007645
alternative hypothesis: two.sided
95 percent confidence interval:
 0.0495782 0.3367854
sample estimates:
   prop 1    prop 2 
0.7272727 0.5340909 
```

$prop 1 = \frac{80}{110} = 0.727$

$prop 2 = \frac{47}{88} = 0.534$

## Other
### median(x)
 
Calculates the **median** of a dataset `x`.

```r
data <- c(8, 7, 6, 9, 4, 2)
median(data)
> [1] 6.5
```

### quantile(x, percentile)

Calculates the correct quantile for the given percentile. In the example below we calculate the value of the 50% percentile. This equals the **median** from the example above.

```r
data <- c(8, 7, 6, 9, 4, 2)
quantile(data, 0.5)
> 50% 
> 6.5
```

### sample(x, n)

Takes a random sample of size `n` from the dataset `x`.

```r
data <- c(8, 7, 6, 9, 4, 2)
sample(data, 3)
> [1] 7 8 6
```

### mean(x)
 
Calculates the **mean** of a dataset `x`.

```r
data <- c(8, 7, 6, 9, 4, 2)
mean(data)
> [1] 6
```

### sd(x)

Caclulates the **standard deviation** of a dataset `x`.

```r
data <- c(8, 7, 6, 9, 4, 2)
sd(data)
> [1] 2.607681
```

### seq(from = 1, to = 1, by = ((to - from)/(length.out - 1))

Generates a sequence from a start-value `from` to an end-value `to` with a step-size `by`. The step-size is added to the start-value until the end-value is reached.

```r
seq(0, 1, 0.1)
> [1] 0.0 0.1 0.2 0.3 0.4 0.5 0.6 0.7 0.8 0.9 1.0
```

### length(x)

Calculates the length of a dataset.

```r
data <- c(1, 2, 3, 4, 5, 6)
length(data)
> [1] 6
```

### choose(n, k)

Calculates the binomial coefficient.

```r
choose(52, 5)
> [1] 2598960
```

### sum(x)

Calculates the sum of a dataset.

```r
data <- 1:100
sum(data)
> [1] 5050
```

### hist(x)

The function computes a histogram of the given data values.

### stripchart(x)

Generates a strip-chart.

## Sources
https://www.rdocumentation.org/
