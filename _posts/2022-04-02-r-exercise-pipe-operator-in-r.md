---
title:  "R Exercise: Pipe Operater In R"
date:   2022-03-18 09:29:17 +0545
categories: R Exercise
tags:
  - Data Analysis
  - R
  - Pipe Operator
header:
  teaser: "assets/r_exercises/association-rule/unnamed-chunk-9-1.png"
  overlay_image: "assets/r_exercises/association-rule/unnamed-chunk-9-1.png"
toc: true
---
# Data Analysis Using Pipe Operator in R

## What is pipe oprator
Pipe operators are a strong tool for expressing a series of numerous operations in a clear and concise manner. The pipe is part of the'magrittr' package. Pipe allows us to write code in a more readable and understandable manner.


## Why to use Pipe

Because R is a functional language, complicated programming frequently necessitates a lot of parenthesis, which means we have to nest those parenthesis together for statistical computing. R codes are difficult to read and comprehend as a result of this. This is when the suitation pipe comes in handy. Pipe operators are divided into three categories. They are,

### %< >% Compound Operator
Updates values for same variable.

```r
x <- rnorm(100)
x %<>% abs %>% sort
x
```
Here at first %<>% find absolute values of x and and then it sort in uncreasing order.

### %>% tee Operator

The plot command normally finishes the code, but the "tee" pipe operator permits it to continue for the next argument.

```r
set.seed(123) 
rnorm(200) %>% 
matrix(ncol = 2) %T>% 
plot %>% 
colSums
```


### %$%

This operator comes in handy when we wish to pipe a dataframe with a lot of columns into a function that only affects a few of them.


```r
data.frame(z = rnorm(100)) %$%
ts.plot(z)
```


## Let's do some Data Analysis in R's Builtin data iris with Pipe Operator

First, let's us check what attributes `iris` data contains.

```r
library(magrittr)
iris
```

`iris` data have four columns they are `Sepal.Length,Sepal.Width, Petal.Length ,Petal.Width Species`. 


```r
library(dplyr)
iris %>%
  select(contains('Sepal')) %>%
  mutate(Sepal.Area=Sepal.Length * Sepal.Width)
```

`contains` function only select those columns which contains **sepal** word. Here we also import `library(dplyr)` dplyr packages is mainly used for data cleaning purpose. It contaims five buitin function they are: 

* select

* filter

* arrange
 
* mutate

These five functions can do majority of data manipulatlation for data analysis task.

In above code mutate function added new column ("Sepal.Area") in the data frame.

```r
iris %>%
  select(starts_with('Sepal')) %>%
  filter(Sepal.Length >= 5.0) %>%
  arrange(Sepal.Length)
``` 

We want to select only those columns that have **Sepal** as a prefix and filter those values that have values greater than 'Sepal.Length >= 5.0', and then we want to arrange them in ascending order using the aforementioned code. To sort in ascending order, just write **desc** into the arrange function, as seen below.


```r
iris %>%
  select(starts_with('Sepal')) %>%
  filter(Sepal.Length >= 5.0) %>%
  arrange(desc(Sepal.Length))
```

## Let's try one Different Step

Let us observer what will come in result if we use `end_with` in place of `starts_with`.

```r
iris %>%
  select(ends_with('Length')) %>%
  rowwise() %>%
  mutate(Length.Diff = Sepal.Length- Petal.Length)
```

I'm hoping we've noticed anything new that's arrived. **Length** is the prefix we have here. It means we only got columns with length as their prefix. We also generated a new column **Length.Diff** using the mutate function.

## Use `transmute` function 


```r
iris %>%
  select(contains('Sepal'), Species) %>%
  transmute(Sepal.Area= Sepal.Length * Sepal.Width)
```

Here **transmute** funtion only show new columns it hide Sepal.Length and Sepal.Width columns.

## What a difference we observe when we use pipe operator and genral R function
Let's clearify it from code


### Using R general function


Assign value of x with given column vector

```r
x <- c(0.109, 0.359, 0.63, 0.996, 0.515, 0.142, 0.017, 0.829, 0.907)
```

Here we want to compute the following with in single line of code,

*  Compute the logarithm of `x`,

*  return suitably lagged and iterated difference

* compute the exponential function and round the result


```r
round(exp(diff(log(x))), 1)

```
Let's to some code using pipe operators.


```r
x %>%log() %>%
  diff() %>%
  exp()%>%
  round(1)
```
Because we didn't require a lot of parentheses in the above pipe, it came together quickly. Finally, we arrived at the same conclusion.

However, while there are numerous benefits to using a pipe operator, there are some criteria to consider. Some of pipe operators' restrictions are listed below.

* Our pipes are more than ten steps long.

* We have a lot of inputs and outputs.

* We're considering a directed graph with a complicated dependence structure.

* We're working on a package internally.

We do not prefer to employ the pipe operator in the instances mentioned above.
















