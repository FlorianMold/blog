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
  - [Uniformverteilung](#uniformverteilung)
    - [dunif(x, min = 0, max = 1, log = FALSE)](#dunifx-min--0-max--1-log--false)
    - [punif(q, min = 0, max = 1, lower.tail = TRUE, log.p = FALSE)](#punifq-min--0-max--1-lowertail--true-logp--false)
    - [qunif(p, min = 0, max = 1, lower.tail = TRUE, log.p = FALSE)](#qunifp-min--0-max--1-lowertail--true-logp--false)
    - [runif(n, min = 0, max = 1)](#runifn-min--0-max--1)
  - [Poisson distribution](#poisson-distribution)
    - [dpois(x, lambda)](#dpoisx-lambda)
    - [ppois(q, lambda, lower.tail = TRUE)](#ppoisq-lambda-lowertail--true)
    - [qpois(p, lambda, lower.tail = TRUE)](#qpoisp-lambda-lowertail--true)
    - [rpois(n, lambda)](#rpoisn-lambda)
  - [Student t-Verteilung](#student-t-verteilung)
    - [dt(x, df)](#dtx-df)
    - [pt(q, df, lower.tail = TRUE)](#ptq-df-lowertail--true)
    - [qt(p, df, lower.tail = TRUE)](#qtp-df-lowertail--true)
    - [rt(n, df)](#rtn-df)
  - [f-distribution](#f-distribution)
    - [df(x, df1, df2)](#dfx-df1-df2)
    - [pf(q, df1, df2, lower.tail = TRUE)](#pfq-df1-df2-lowertail--true)
    - [qf(p, df1, df2, lower.tail = TRUE)](#qfp-df1-df2-lowertail--true)
    - [rf(n, df)](#rfn-df)
  - [$Chi^2$ Distribution](#chi2-distribution)
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
    - [stripchard(x)](#stripchardx)
  - [Sources](#sources)

Functions that start with:
- `d` return the **Probability Mass Function** (PMF) for discrete distributions and the **Probability Density Function** (PDF) for continuos distributions
- `p` return the **Cumulative Density Function** (CDF).
- `q` return the value at a given quantile.
  - 99.5

## Important parameters:
- **lower.tail**: Gibt an, welcher Bereich berechnet wird. Entweder wird der Bereich unter einem Wert berechnet oder der Bereich über Wert.
  - `lower.tail = TRUE` (default): 
    - P(X <= x) is calculated  
  - `lower.tail = FALSE`:
    - P(X > x) is calculated

## Normal distribution

- **mean**: Mean
- **sd**: Standard deviation

### dnorm(x, mean = 0, sd = 0)

`x` ist der Wert, für den ich die Wahrscheinlichkeit möchte. Im unteren Beispiel beispiel berechne ich die Wahrscheinlichkeit, dass 0 als Wert herauskommt.

```r
mean <- 0
sd <- 1

# Gibt mir die Wahrscheinlichkeit, dass GENAU 0 bei einer Standardnormalverteilung herauskommt
dnorm(0, mean, sd)
> [1] 0.3989
```

### pnorm(q, mean = 0, sd = 0, lower.tail = TRUE)

`q` ist der Wert bis zu dem wir die Wahrscheinlichkeit berechnen möchten. Man berechnet also die Wahrscheinlichkeit für q oder weniger **P(X <= q)**. Wenn man `lower.tail = FALSE` setzt, dann berechnet man den oberen Teil. Also wird **P(X > q)** berechnet oder auch **1 - P(X <= q)**.

*lower.tail = TRUE*:
```r
mean <- 170
sd <- 25

# Gibt mir die Wahrscheinlichkeit, die Größe 170 oder weniger zu haben (-infty, 170). 
# Da der Wert dem Mean entspricht liegt dieser Wert genau in der Mitte, weshalb 50% herauskommt. 
# Da 50% der Verteilung links von diesem Wert liegen.
pnorm(170, mean, sd)
> [1] 0.5
```
*lower.tail = FALSE*:
```r
mean <- 170
sd <- 25

# Gibt mir die Wahrscheinlichkeit, größer als 170 sein (X > 170). 
# Da der Wert dem Mean entspricht liegt dieser Wert genau in der Mitte, weshalb 50% herauskommt. 
# Da 50% der Verteilung rechts von diesem Wert liegen.
pnorm(170, mean, sd, lower.tail=FALSE)
> [1] 0.5
```

```r
mean <- 170
sd <- 25

# Gibt mir die Wahrscheinlichkeit, zwischen 150cm und 170cm groß zu sein.
pnorm(170, mean, sd) - pnorm(150, mean, sd)
> [1] 0.2881446
```

Diese Berechnung ist äquivalent zu dem, wenn ich etwas aus den Tabellen der Normalverteilung herauslese.

**IQR (Inner Quartile Range)**:

- Wert bei 75% der Verteilung - Wert bei 25% der Verteilung
- $Q_3$ - $Q_1$ (75% - 25%)
- ```qnorm(0.75, mean, sd) - qnorm(0.25, mean, sd)```


### qnorm(p, mean = 0, sd = 0, lower.tail = TRUE)

p ist der Wert eines Percentil an dem ich den Wert berechnen möchte. Wenn ich beispielsweise berechnen möchte wie groß 50% der Menschen maximal sind: 

*lower.tail = TRUE*:
``` r
mean <- 170
sd <- 25

# Gibt mir den Wert, wo 50% der Verteilung vorbei sind. 
# Bei einer Größenverteilung wäre das 170, da dieser Wert der Mean ist und genau in der Mitte liegt.
# Das heißt 50% der Menschen sind <= 170cm
qnorm(0.5, mean, sd)
> [1] 170
```
Das liefert mir den Wert wenn ich bei der Verteilung von links zu schauen beginne. Also von links, wo sind 50% der Verteilung vorbei.

Wenn ich mit `lower.tail = FALSE` arbeite, dann beginne ich bei der Verteilung von rechts zu schauen. Also von rechts weg wo 60% der Verteilung vorbei sind.
*lower.tail = FALSE*:
``` r
mean <- 170
sd <- 25

# Gibt mir den Wert, wo 60% der Verteilung vorbei sind. 
# Bei einer Größenverteilung wäre das 176.3337. Das heißt 60% der Menschen sind <= 170cm
qnorm(0.6, mean, sd, lower.tail=TRUE)
> [1] 176.3337

# Wir schauen bei der Verteilung von rechts aus schauen, wo 60% der Verteilung vorbei sind. 
# Dieses Ergebnis wäre gleich zu der Berechnung von ich von links aus 40% schaue.
qnorm(0.6, mean, sd, lower.tail=FALSE)
> [1] 163.6663

# Gleiches Ergebnis wie im oberen Beispiel, da wir von links weg 40% schauen. 
# Oben haben wir von rechts weg 60% geschaut, was ja gleich ist zu den 40% von links.
qnorm(0.4, mean, sd)
> [1] 163.6663
```

Diese Berechnung wäre das verkehrt herum herauslesen aus den Tabellen der Standardnormalverteilungen. Also aus den Prozenten den Wert heraulesen.

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

- **x**: Anzahl der erfolgreichen Versuche für die wir die Wahrscheinlichkeit suchen
- **size**: Insgesamte Anzahl der Versuche
- **prob**: Wahrscheinlichkeit für einen erfolgreichen Versucht

### dbinom(x, size, prob)

x ist die Anzahl der erfolgreichen Versuche für die wir die Wahrscheinlichkeit suchen. Mit dieser Funktion berechne ich den Wert einer PMF an der Stelle x. Im unteren Beispiel berechne ich die Wahrscheinlichkeit, bei 10 Münzwürfen genau 5 Köpfe zu bekommen.

```r
n <- 10
prob <- 1/2

# WSK bei 10 Würfen genau 5 Köpfe zu bekommen mit einer WSK 50%
dbinom(5, n, prob)
> [1] 0.2460938
```
### pbinom(q, size, prob, lower.tail = TRUE)

`q` ist der Wert bis zu dem wir die Wahrscheinlichkeit berechnen möchten. Man berechnet also die Wahrscheinlichkeit für q oder weniger **P(X <= q)**. Wenn man `lower.tail = FALSE` setzt, dann berechnet man den oberen Teil. Also wird **P(X > q)** berechnet oder auch **1 - P(X <= q)**.

*lower.tail = TRUE*:
```r
n <- 10
prob <- 1/2

# Gibt mir die Wahrscheinlichkeit 5 oder weniger Köpfe zu werfen.
pbinom(5, n, prob)
> [1] 0.6230469
```
*lower.tail = FALSE*:
```r
n <- 10
prob <- 1/2

# Gibt mir die Wahrscheinlichkeit mehr als 5 Köpfe zu werfen. 
# Ist genau die Gegenwahrscheinlichlkeit zu oben.
pbinom(5, n, prob)
> [1] 0.3769531
```

### qbinom(p, size, prob, lower.tail = TRUE)

p ist der Wert eines Percentil an dem ich den Wert berechnen möchte. Wenn ich berechnen möchte, wie viele Köpfe ich mit 60% Wahrscheinlichkeit bekomme.

*lower.tail = TRUE*:
``` r
n <- 10
prob <- 1/2

# Gibt mir die Anzahl der Köpfe, die mit 50% WSK auftreten. 
# 5 Köpfe treten mit einer WSK von 50% auf.
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

## Uniformverteilung

- **x**: Wert im Intervall für den ich den Wert suche
- **min**: Startwert des Intervalls
- **max**: Endwert des Intervalls

### dunif(x, min = 0, max = 1, log = FALSE)
`x` ist der Wert, für den ich die Wahrscheinlichkeit möchte. Beim unteren Beispiel geht es um ein Intervall von 60 Minuten. Ich berechne die Wahrscheinlichkeit, dass der Zug in der 3 Minute kommt. Die Fläche der Uniformverteilung ist genau 1 und ein Rechteck. Daher ist die Wahrscheinlichkeit für, dass der Zug in einer bestimmten Minute kommt immer gleich, egal welche. Aufsummiert ergeben die WSK dann 1.

```r
min <- 0
max <- 60

# Gibt mir die Wahrscheinlichkeit, dass der Zug genau in der dritten Minute kommt. 
# Die Wahrscheinlichkeit ist für jede Minute gleich
dunif(3, min, max)
> [1] 0.01666667
```
### punif(q, min = 0, max = 1, lower.tail = TRUE, log.p = FALSE)

`q` ist der Wert bis zu dem wir die Wahrscheinlichkeit berechnen möchten. Man berechnet also die Wahrscheinlichkeit für q oder weniger **P(X <= q)**. Wenn man `lower.tail = FALSE` setzt, dann berechnet man den oberen Teil. Also wird **P(X > q)** berechnet oder auch **1 - P(X <= q)**.

*lower.tail = TRUE*:
```r
min <- 0
max <- 60

# Gibt mir die Wahrscheinlichkeit, dass der Zug in den ersten 20 Minuten kommt. 
# Dazu einfach die WSK für 1 Minute * 20 rechnen.
punif(20, min, max)
> [1] 0.3333333
```
*lower.tail = FALSE*:
```r
min <- 0
max <- 60

# Gibt mir die Wahrscheinlichkeit, dass der Zug in den letzten 20 Minuten kommt. 
# Hier wird vom Wert 40 nach rechts geschaut in der Verteilung
punif(40, min, max, lower.tail=FALSE)
> [1] 0.3333333
```

### qunif(p, min = 0, max = 1, lower.tail = TRUE, log.p = FALSE)

p ist der Wert eines Percentil an dem ich den Wert berechnen möchte. Hier würden 50% 30 Minuten ergeben, da nach 50% der Verteilung 30 Minuten vergangen sind

*lower.tail = TRUE*:
``` r
min <- 0
max <- 60

# Gibt mir den Wert, wo 50% der Verteilung vorbei sind. 
# Bei einer Stunde wären das 30 Minuten
qunif(0.5, min, max)
> [1] 170
```
Das liefert mir den Wert wenn ich bei der Verteilung von links zu schauen beginne. Also von links, wo sind 50% der Verteilung vorbei.

Wenn ich mit `lower.tail = FALSE` arbeite, dann beginne ich bei der Verteilung von rechts zu schauen. Also von rechts weg wo 60% der Verteilung vorbei sind.
*lower.tail = FALSE*:
``` r
min <- 0
max <- 60

# Gibt mir den Wert, wo 60% der Verteilung vorbei sind. 
# 36 Minuten sind vorbei
qunif(0.6, min, max, lower.tail=TRUE)
> [1] 36

# Wir schauen bei der Verteilung von rechts aus schauen, wo 60% der Verteilung vorbei sind. 
# Dieses Ergebnis wäre gleich zu der Berechnung von ich von links aus 40% schaue. 
# Beide Werte müssen sich insgesamt zu 60 ausgleichen, da so groß das Intervall ist
qunif(0.6, min, max, lower.tail=FALSE)
> [1] 24

# Gleiches Ergebnis wie im oberen Beispiel, da wir von links weg 40% schauen. 
# Oben haben wir von rechts weg 60% geschaut, was ja gleich ist zu den 40% von links.
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

- **lambda**: Wie oft tritt das Event in einem Zeitintervall auf

### dpois(x, lambda)
`x` ist der Wert, für den ich die Wahrscheinlichkeit möchte. Im unteren Beispiel berechne ich die Wahrscheinlichkeit, dass 1 Hurrican in einem Jahr auftritt.

```r
years <- 22
hurricans <- 27

lambda <- hurricans/years # 1.227 hurricans pro Jahr

# Gibt mir die Wahrscheinlichkeit, dass GENAU 1 Hurrikan auftritt
dpois(1, lambda)
> [1] 0.3597024
```
### ppois(q, lambda, lower.tail = TRUE)

`q` ist der Wert bis zu dem wir die Wahrscheinlichkeit berechnen möchten. Man berechnet also die Wahrscheinlichkeit für q oder weniger **P(X <= q)**. Wenn man `lower.tail = FALSE` setzt, dann berechnet man den oberen Teil. Also wird **P(X > q)** berechnet oder auch **1 - P(X <= q)**.

*lower.tail = TRUE*:
```r
years <- 22
hurricans <- 27

lambda <- hurricans/years # 1.227 hurricans pro Jahr

# Gibt mir die Wahrscheinlichkeit, dass weniger als 3 Hurrikans in einem Jahr auftreten.
ppois(2, lambda)
> [1] 0.8735197
```
*lower.tail = FALSE*:
```r
years <- 22
hurricans <- 27

lambda <- hurricans/years # 1.227 hurricans pro Jahr

# Gibt mir die Wahrscheinlichkeit, dass mehr als 2 Hurrikans in einem Jahr auftreten. 
# Dies ist natürlich genau die Gegenwahrscheinlichkeit zu weniger als 3 Hurrikans auftreten.
ppois(2, lambda, FALSE)
> [1] 0.1264803
```

### qpois(p, lambda, lower.tail = TRUE)

p ist der Wert eines Percentil an dem ich den Wert berechnen möchte. Wenn ich beispielsweise berechnen möchte, wie viele Hurrikans mit 99.5% Wahrscheinlichkeit auftreten.

*lower.tail = TRUE*:
``` r
years <- 22
hurricans <- 27

lambda <- hurricans/years # 1.227 hurricans pro Jahr

# Gibt mir die Anzahl der Hurricans, die mit 99.5% WSK in einem Jahr auftreten. 
# 5 oder weniger Hurrikans treten mit einer WSK von 99.5% in einem Jahr auf
qpois(0.995, e)
> [1] 5
```

### rpois(n, lambda)

This function takes `n` samples from the given poisson distribution. Below we take 5 samples from a poisson distribution with lambda 27/22.

``` r
years <- 22
hurricans <- 27

lambda <- hurricans/years # 1.227 hurricans pro Jahr

# Returns 5 samples of how many hurricans can occur in one year.
rpois(5, lambda)
> [1] 0 4 2 2 2
```

## Student t-Verteilung

- **df**: Freiheitsgrade, normalerweise n-1

### dt(x, df)

`x` ist der Wert, für den ich die Wahrscheinlichkeit möchte. Zusäztlich benötige ich im unteren Beispiel die Freiheitsgrade. Diese berechnen sich normalerweise aus der Sample Size - 1. Im unteren Beispiel beispiel berechne ich die Wahrscheinlichkeit, dass 0 als Wert herauskommt.

```r
mean <- 0
sd <- 1

# Gibt mir die Wahrscheinlichkeit, dass GENAU 0 bei einer t-Verteilung herauskommt
dt(0, 10)
> [1] 0.3891084

dt(0, 200)
> [1] 0.3984439

dnorm(0)
> [1] 0.3989423

# Wie man sieht nähert sich  die t-Verteilung immer weiter der Normalverteilung an, umso höher die Sample
# Size ist
```

### pt(q, df, lower.tail = TRUE)

`q` ist der Wert bis zu dem wir die Wahrscheinlichkeit berechnen möchten. Man berechnet also die Wahrscheinlichkeit für q oder weniger **P(X <= q)**. Wenn man `lower.tail = FALSE` setzt, dann berechnet man den oberen Teil. Also wird **P(X > q)** berechnet oder auch **1 - P(X <= q)**.

*lower.tail = TRUE*:
```r
# Gibt mir die Wahrscheinlichkeit, den Wert 1 oder weniger in der Standardnormalverteilung zu haben.
pnorm(1)
> [1] 0.8413447

# Gibt mir die Wahrscheinlichkeit, den Wert 1 oder weniger zu haben. 
# Hier sind die 10 Freiheitsgrade zu beachten. 
# Wie man sieht ist der Wert schon sehr nahe bei dem Wert der Standardnormalverteilung
pt(1, 10)
> [1] 0.8295534

# Gleiche Berechnung wie oben, aber mit 200 Freiheitsgraden. 
# Wert ist deutlich näher beim Wert der Standardnormalverteilung.
pt(1, 200)
> [1] 0.8407406
```

*lower.tail = FALSE*:
```r
# Gibt mir die Wahrscheinlichkeit, mehr als den Wert 1 zu haben. 
# Dies ist genau die Gegenwahrscheinlichkeit zu oben.
pt(1, 10, lower.tail=FALSE)
> [1] 0.1592594

pt(1, 200, lower.tail = FALSE)
> [1] 0.1592594
```

### qt(p, df, lower.tail = TRUE)

p ist der Wert eines Percentil an dem ich den Wert berechnen möchte. 

*lower.tail = TRUE*:
``` r

# Gibt mir den Wert, wo 60% der Verteilung vorbei sind. 
qnorm(0.6)
> [1] 0.2533471

# Gibt mir den Wert, wo 60% der Verteilung vorbei sind. 
# Man beachte die 10 Freiheitsgrade. Wert liegt schon sehr nahe bei dem der Standardnormalverteilung
qt(0.6, 10)
> [1] 0.2601848

# Gibt mir den Wert, wo 60% der Verteilung vorbei sind. 
# Man beachte die 200 Freiheitsgrade.
# Wert ist noch näher bei der Standardnormalverteilung
qt(0.6, 200)
> [1] 0.2536844
```
Das liefert mir den Wert wenn ich bei der Verteilung von links zu schauen beginne. Also von links, wo sind 60% der Verteilung vorbei.

Wenn ich mit `lower.tail = FALSE` arbeite, dann beginne ich bei der Verteilung von rechts zu schauen. Also von rechts weg wo 60% der Verteilung vorbei sind.
*lower.tail = FALSE*:
``` r
# Gibt mir den Wert, wo 60% der Verteilung vorbei sind. 
qt(0.6, 200, lower.tail=TRUE)
> [1] 0.2536844

# Wir schauen bei der Verteilung von rechts aus, wo 60% der Verteilung vorbei sind. 
# Dieses Ergebnis wäre gleich zu der Berechnung wenn ich von links aus 40% schaue.
qt(0.6, 200, lower.tail=FALSE)
> [1] -0.2536844

# Gleiches Ergebnis wie im oberen Beispiel, da wir von links weg 40% schauen. 
# Oben haben wir von rechts weg 60% geschaut, was ja gleich ist zu den 40% von links.
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

`x` ist der Wert, für den ich die Wahrscheinlichkeit möchte. Zusäztlich benötige ich im unteren Beispiel die Freiheitsgrade. Im unteren Beispiel berechne ich die Wahrscheinlichkeit, dass 0 als Wert herauskommt.

```r
# Gibt mir die Wahrscheinlichkeit, dass GENAU 1 bei einer f-Verteilung herauskommt
df(1, 10, 10)
> [1] 0.6152344
```

### pf(q, df1, df2, lower.tail = TRUE)

`q` ist der Wert bis zu dem wir die Wahrscheinlichkeit berechnen möchten. Man berechnet also die Wahrscheinlichkeit für q oder weniger **P(X <= q)**. Wenn man `lower.tail = FALSE` setzt, dann berechnet man den oberen Teil. Also wird **P(X > q)** berechnet oder auch **1 - P(X <= q)**.

*lower.tail = TRUE*:
```r
# Gibt mir die Wahrscheinlichkeit, den Wert 2 oder weniger zu haben. 
# Hier sind die 10 Freiheitsgrade zu beachten. 
pf(1, 10, 10)
> [1] 0.8551542
```

*lower.tail = FALSE*:
```r
# Gibt mir die Wahrscheinlichkeit, mehr als den Wert 2 zu haben. 
# Dies ist genau die Gegenwahrscheinlichkeit zu oben.
pt(2, 10, lower.tail=FALSE)
> [1] 0.1448458
```

### qf(p, df1, df2, lower.tail = TRUE)

p ist der Wert eines Percentil an dem ich den Wert berechnen möchte. 

*lower.tail = TRUE*:
``` r
# Gibt mir den Wert, wo 60% der Verteilung vorbei sind. 
# Man beachte die 10 Freiheitsgrade.
qf(0.6, 10, 10)
> [1] 1.178651

```
Das liefert mir den Wert wenn ich bei der Verteilung von links zu schauen beginne. Also von links, wo sind 60% der Verteilung vorbei.

### rf(n, df)

This function takes `n` samples from the given f-distribution. Below we take 5 samples from a f-distribution with 10 degrees of freedom.

``` r
rf(5, 10, 10)
[1] 3.1506333 1.4209381 3.4736313 0.3532966 1.3175930
```

## $Chi^2$ Distribution

```r
qchisq(0.99,2)
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

$prop 2 = \frac{47}{88} = 0.0.534$

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

### stripchard(x)

Generates a strip-chart.

## Sources
https://www.rdocumentation.org/
