---
title:  "R Exercise: Different Hypothesis Testing in R"
date:   2022-06-03 09:29:17 +0545
categories: R Exercise
tags:
  - Data Analysis
  - R
  - linear Model
header:
  teaser: "assets/header_images/Rlogo.png"
  overlay_image: "assets/header_images/Rlogo.png"
toc: true
---
## What is Hypothesis Testing

It is a type of inferential statistics that involves extrapolating
results from a sample (random) to the entire population. It’s used to
make decisions based on statistical tests and models that use the
p-value, also known as the Type I error or alpha error.

**Type I Error** : When we reject true null hypothesis then it is called
`type I error`

**Type II Error** : When we do not reject false null hypothesis then it
is called type II error.

It can be done using parametric or non-parametric methods/models.

**Parametric** : They have certain assumptions about the data (model)
and/or errors that must be validated before the results can be accepted.

**Non-parametric** : They are non-parametric because they make no
assumptions about the data distribution (model) or mistakes.

## Why to use parametric test?

Because they are based on the mean, standard deviation, and normal
distribution, parametric tests are regarded “more powerful” than non
parametric tests/models. Non-parametric tests are based on median, IQR,
and non-normal distributions, non-parametric tests are deemed “less
powerful” than parametric tests/models.

## Two Statistical Hypothesis

`Null Hypothesis` : It is also known as hypothesis of no difference
`Alternative Hypothesis` : It is complementary to the null hypothesis
also known as research hypotheis.

## When to accept Null or Alternative Hypothesis

Accept (fail to reject) null hypothesis from parametric or
non-parametric tests requires a P-value \> 0.05. (Goodness-of-fit tests)

To accept it from parametric or non-parametric testing (Research
hypothesis tests! ), the P-value must be less than 0.05.

# Some Commonly Used Parametric Test Using R

## One Sample Z Test On Mtcars Data

In this blog I am only going to explain how to test one sample z test
using R without explain what is z-test, how it work because I already
explained it in my past blog.

``` r
# we need to define parameter
muO <- 20
sigma <- 6
xbar <- mean(mtcars$mpg)
n <- length(mtcars$mpg)
z <-sqrt(n)*(xbar-muO)/sigma
p_value<-2*pnorm(-abs(z))
```

Let’s check z value and p value,

``` r
z
```

    ## [1] 0.08544207

Hence, we found value of z is 0.08544207

``` r
p_value
```

    ## [1] 0.9319099

We found p-vale 0.9319099 which is > 0.05 hence we accpet null
hypothesis, i.e means of sample and population are equal.

## Why there is no one sample z-test in base R package?

Because the t-distribution behaves like the z-distribution for n>=30,
the T-test can be employed for both small and big samples. Thus, we
don’t need one-sample z-test in R!

# One Sample t-test: We can work for small sample as well as for large sample

``` r
t.test(mtcars$mpg, mu =20)
```

    ## 
    ##  One Sample t-test
    ## 
    ## data:  mtcars$mpg
    ## t = 0.08506, df = 31, p-value = 0.9328
    ## alternative hypothesis: true mean is not equal to 20
    ## 95 percent confidence interval:
    ##  17.91768 22.26357
    ## sample estimates:
    ## mean of x 
    ##  20.09062

Hence we obtained p-valued 0.9328 it means we do not reject null
hypothesis.

## Two Sample T-test

It is used to compare the means of a dependent variable with two
categories of grouped independent variables. For instance, we can
compare exam score (dependent variable) between male and female groups
of students!

*Assumptions*

-   For each category, the dependent variable must follow the normal
    distribution (Test of normality-GOF)

-   The variance is homogeneous (i.e. equal) across independent variable
    categories (Test of equal variance-GOF)

## What to do if variance across independent variable categories not equal

In this case we used Welch test.

*Assumption*

-   For each category, the dependent variable must follow the normal
    distribution (Test of normality-GOF)

-   Variance across independent variable categories are not homogenous
    i.e; not equal.

## Let’s do narmality test on mtcars data

``` r
with(mtcars, shapiro.test(mpg[am == 0]))
```

    ## 
    ##  Shapiro-Wilk normality test
    ## 
    ## data:  mpg[am == 0]
    ## W = 0.97677, p-value = 0.8987

Here, p-value is 0.8987. Hence, we do not reject null hypothesis that
means it follows normal distribution.

``` r
with(mtcars, shapiro.test(mpg[am == 1]))
```

    ## 
    ##  Shapiro-Wilk normality test
    ## 
    ## data:  mpg[am == 1]
    ## W = 0.9458, p-value = 0.5363

It also follows normal distribution. Hence first condition is satisfied
i.e; dependent variable mpg follows normal distribution.

## Variance Check

``` r
var.test(mpg ~ am, data = mtcars)
```

    ## 
    ##  F test to compare two variances
    ## 
    ## data:  mpg by am
    ## F = 0.38656, num df = 18, denom df = 12, p-value = 0.06691
    ## alternative hypothesis: true ratio of variances is not equal to 1
    ## 95 percent confidence interval:
    ##  0.1243721 1.0703429
    ## sample estimates:
    ## ratio of variances 
    ##          0.3865615

We can see p-value is 0.06691 which is grater than 0.05. Hence we can
say variance across independent variable categories are same. Now we can
use two sample student t test.

``` r
t.test(mpg ~ am, var.equal= T, data = mtcars)
```

    ## 
    ##  Two Sample t-test
    ## 
    ## data:  mpg by am
    ## t = -4.1061, df = 30, p-value = 0.000285
    ## alternative hypothesis: true difference in means between group 0 and group 1 is not equal to 0
    ## 95 percent confidence interval:
    ##  -10.84837  -3.64151
    ## sample estimates:
    ## mean in group 0 mean in group 1 
    ##        17.14737        24.39231

Here we saw p-value 0.000285 which is less then 0.05. Hence we reject ho
that means milage (mpg) is statistically different among cars with
automatic and manual transmission system.

## Let’s check two sample student t-test result with simple linear regression model

``` r
summary(lm(mpg ~ am, data = mtcars))
```

    ## 
    ## Call:
    ## lm(formula = mpg ~ am, data = mtcars)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -9.3923 -3.0923 -0.2974  3.2439  9.5077 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)   17.147      1.125  15.247 1.13e-15 ***
    ## am             7.245      1.764   4.106 0.000285 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 4.902 on 30 degrees of freedom
    ## Multiple R-squared:  0.3598, Adjusted R-squared:  0.3385 
    ## F-statistic: 16.86 on 1 and 30 DF,  p-value: 0.000285

This difference is statistically significant and the p-value is same as
given by the two-samples t-test.

# What test should we used if we have to compare mean of more than two samples

If we need to compare mean of more than two samples we used 1-way ANOVA
test.

*Assumption*

-   Dependent variable must be “normally distributed”

-   Variance across categories must be same

# 1-way ANOVA assumptions checks

Normality by categories

``` r
with(mtcars, shapiro.test(mpg[gear == 3]))
```

    ## 
    ##  Shapiro-Wilk normality test
    ## 
    ## data:  mpg[gear == 3]
    ## W = 0.95833, p-value = 0.6634

Category 3 follows normal distribution.

``` r
with(mtcars, shapiro.test(mpg[gear == 4]))
```

    ## 
    ##  Shapiro-Wilk normality test
    ## 
    ## data:  mpg[gear == 4]
    ## W = 0.90908, p-value = 0.2076

Category 4 also follows normal distribution.

``` r
with(mtcars, shapiro.test(mpg[gear == 5]))
```

    ## 
    ##  Shapiro-Wilk normality test
    ## 
    ## data:  mpg[gear == 5]
    ## W = 0.90897, p-value = 0.4614

So, dependent variable follows normal distribution.

## Let’s do variance test

In case of more than two samples case we do not use
`var.test()`. For this we used`leveneTest()` avilable in car packages.
Let’s check. Before doing this we need to change our independent
variable into factor.

``` r
library(car)
```

    ## Loading required package: carData

``` r
leveneTest(mpg ~ as.factor(gear), data=mtcars)
```

    ## Levene's Test for Homogeneity of Variance (center = median)
    ##       Df F value Pr(>F)
    ## group  2  1.4886 0.2424
    ##       29

Here, we find p-value grater than 0.2424. Hence variance across
categories is same. So, we can now used one way calssical ANOVA test.

## 1-Way Classical ANOVA test

``` r
summary(aov(mpg ~ gear, data = mtcars))
```

    ##             Df Sum Sq Mean Sq F value Pr(>F)   
    ## gear         1  259.7  259.75   8.995 0.0054 **
    ## Residuals   30  866.3   28.88                  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

We find p-value less than 0.05. Hence we reject null hypothesis that
means sample means are not equal. This means, post-hoc test or pairwise
comparison is required. If alternative hypothesis is accepted we need to
do post-hoc test. For classical 1-way ANOVA TukeyHSD post-hoc test is
best. Let’s used it.

``` r
TukeyHSD(aov(mpg ~ as.factor(gear), data = mtcars))
```

    ##   Tukey multiple comparisons of means
    ##     95% family-wise confidence level
    ## 
    ## Fit: aov(formula = mpg ~ as.factor(gear), data = mtcars)
    ## 
    ## $`as.factor(gear)`
    ##          diff        lwr       upr     p adj
    ## 4-3  8.426667  3.9234704 12.929863 0.0002088
    ## 5-3  5.273333 -0.7309284 11.277595 0.0937176
    ## 5-4 -3.153333 -9.3423846  3.035718 0.4295874

## Let’s check this result with simple linear model

``` r
summary(lm(mpg ~ gear, data = mtcars))
```

    ## 
    ## Call:
    ## lm(formula = mpg ~ gear, data = mtcars)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -10.240  -2.793  -0.205   2.126  12.583 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)   
    ## (Intercept)    5.623      4.916   1.144   0.2618   
    ## gear           3.923      1.308   2.999   0.0054 **
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 5.374 on 30 degrees of freedom
    ## Multiple R-squared:  0.2307, Adjusted R-squared:  0.205 
    ## F-statistic: 8.995 on 1 and 30 DF,  p-value: 0.005401

``` r
pairwise.t.test(mtcars$mpg, mtcars$gear, p.adj= "none")
```

    ## 
    ##  Pairwise comparisons using t tests with pooled SD 
    ## 
    ## data:  mtcars$mpg and mtcars$gear 
    ## 
    ##   3       4    
    ## 4 7.3e-05 -    
    ## 5 0.038   0.218
    ## 
    ## P value adjustment method: none

gear = 3 category is omitted from the result because R automatically
creates 3 dummy variables for 3 categories of gear variable i.e. 3, 4
and 5 and uses only last two of them in the model and takes the first
one as reference.
