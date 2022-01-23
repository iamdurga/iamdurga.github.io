---
title:  "Dataframe in R."
date:   2021-11-8 01:29:17 +0545
categories: R Basic
tags:
  - R
  - Beginner
header:
  teaser: "assets/header_images/Rlogo.png"
  overlay_image: "assets/header_images/Rlogo.png"
toc: true
---


# Getting Started With Dataframe.

## Introduction
 Dataframe are the mostly used data structure in R. Dataframe is a list where all components have name and are on the same line. Easiest way of understanding about dataframe is the visualization of spreadsheets. The first row is represented by header. The header is given by the list component name. Each column can store the different datatype which is called a variable and each row is an observation across multiple variables, since dataframe are like spreadsheet we can insert the data how we will like to. There are many possibilities to inserting data.

| Product | apple | Banana|
|----------|-------|-------|
|price store A| 23 | 56|
| price store B | 67| 80|

It is not dataframe because here price store is divided into two parts. If we rearrange the data by taking product is one variable and price is next variable  and store is one variable then it become dataframe.

|Product | Price | Store|
|--------|--------|-----|
|apple|23|A|
|apple|67|B|
|banana|56|A|
|banana|80|B|

### Attributes of dataframe
* Length
* Dimension
* Name
* Class  
## How to Create DataFrame

```R
product <- c('apple','banana','orange','papaya','rice','wheat','pee','noodle')
catagory <- c( 'groceries','groceries','electronic','electronic','groceries','electronic','electronic','groceries')
price <- c(24,45,67,88,56,78,89,90)
quality <- c('high','low','high','low','high','low','high','low') 
```

 To create dataframe from above data we can do

 ```R
 shopping_data <- data.frame(product,catagory,price,quality,
                           budget = c(120,3000,600,500,45,67,89,90))
shopping_data
```

Output of the avove code is, dataframe.

To check wether it is dataframe or not we can use folowing code.

```R 
str(shopping_data)
```

Output of the above cde is,

```R
'data.frame':	8 obs. of  5 variables:
 $ product : chr  "apple" "banana" "orange" "papaya" ...
 $ catagory: chr  "groceries" "groceries" "electronic" "electronic" ...
 $ price   : num  24 45 67 88 56 78 89 90
 $ quality : chr  "high" "low" "high" "low" ...
 $ budget  : num  120 3000 600 500 45 67 89 90 
 ```

 ### Check the attribute of dataframe.
 
 ```R
 names(shopping_data)
 ```
 
 ### Check dimension of dataframe.
 ```R
 dim(shopping_data)
 ```
 
 ### Check first six rows of dataframe
 ```R
 head(shopping_data)
 ```
 
 ### Check last six rows of dataframe.
 ```R
 tail(shopping_data)
 ```
 
 ### Take only two rows of dataframe.
 ```R
 head(shopping_data, n =  2)
 ```
 
 ### Access specified column of database.
 ```R
 shopping_data$product
 ```
 
 Output of the above code is,
 ```R
 'apple''banana''orange''papaya''rice''wheat''pee''noodle'
 ```
 
 ```R
 shopping_data[['product']]
 ```
 
 Output of the above code is,
 ```R
 'apple''banana''orange''papaya''rice''wheat''pee''noodle'
 ```

##  Manipulating dataframe
By manipulating data frame we khow how to select, add new row and how to sort and rank into dataframe. Dataframe are list where each elements are name vector of same length. Therefore we can select element as same as in list. we do by [[]] or $column. Dataframe are also two dimensional matricies which means we can index them as matrices by using square braces.[row,column].We fix data in one dimension they behave as list. Therefore dataframe can be index either as like list or as like matrices accoding to positions, rules, names.

### List subsetting
```R 
#list subsetting
shopping_data[[2]]
shopping_data[['budget']]
shopping_data$price
shopping_data$price[1:3]
shopping_data[[3]][3]
shopping_data$price[3]
```

Output of the above code is,
```R
'groceries''groceries''electronic''electronic''groceries''electronic''electronic''groceries'
120300060050045678990
2445678856788990
244567
67
67
```

### Matrix subsetting
```R
#Matrix subsetting
shopping_data[,1]
shopping_data[,"product"]
shopping_data[1,]
shopping_data[1,"price"]
```

Output will be 
```R
'apple''banana''orange''papaya''rice''wheat''pee''noodle'
'apple''banana''orange''papaya''rice''wheat''pee''noodle'
A data.frame: 1 × 5
1	apple	groceries	24	high	120
24
```

### Add new attribute into dataframe.

```R
feedback<- c('good','outstanding','ordinary','nice','excilent','brillent','extra-ordinary','satisfactory')
shopping_data <- cbind(shopping_data,feedback)
shopping_data
```

Output will be

```R
A data.frame: 8 × 6
apple	groceries	24	high	120	good
banana	groceries	45	low	3000	outstanding
orange	electronic	67	high	600	ordinary
papaya	electronic	88	low	500	nice
rice	groceries	56	high	45	excilent
wheat	electronic	78	low	67	brillent
pee	electronic	89	high	89	extra-ordinary
noodle	groceries	90	low	90	satisfactory
```
### We can do the following operations to access the data from dataframe

```R
shopping_data[c(1:3),1]
shopping_data[1]
shopping_data[[1]]
is.vector(shopping_data[1])
is.vector(shopping_data[[1]])
is.list(shopping_data[1])
is.list(shopping_data[1])
```

Output is,

```R
'apple''banana''orange'
A data.frame: 8 × 1
apple
banana
orange
papaya
rice
wheat
pee
noodle
'apple''banana''orange''papaya''rice''wheat''pee''noodle'
FALSE
TRUE
TRUE
TRUE
```

##  Working with tidyverse

During data analysis we spend our most time in data cleaning and transforming the raw data. Tydyverse is an add on that let us perform operation such as cleaning data and creating powerful graph.

```R
product <- c('apple','banana','orange','papaya','Rice','wheat','pee','noodle')
catagory <- c( 'groceries','groceries','electronic','electronic','groceries','electronic','electronic','groceries')
price <- c(24,45,67,88,56,78,89,90)
quality <- c('high','low','high','low','high','low','high','low')
shopping_data <- data.frame(product,catagory,price,quality,
                           budget = c(120,3000,600,500,45,67,89,90))
#arrange(desc(price))
shopping_data
```

Output is,

```R
A data.frame: 8 × 5
apple	groceries	24	high	120
banana	groceries	45	low	3000
orange	electronic	67	high	600
papaya	electronic	88	low	500
Rice	groceries	56	high	45
wheat	electronic	78	low	67
pee	electronic	89	high	89
noodle	groceries	90	low	90
```
### Select Function

Select function allow us to select specified data from dataframe.

```R
# dplyr never change the original data
#install.packages("tidyverse")
#library(tidyverse)
library(dplyr) 
product <- select(shopping_data,price,budget)
product
```
Output is,
```R

A data.frame: 8 × 2
24	120
45	3000
67	600
88	500
56	45
78	67
89	89
90	90
```
### Filter

Filter function work similar to the select. Using the pipe operator %>% we can write multiple operations at once without renaming the intermedating results.

```R
filter(product,budget > 100)
```

Output is,

```R
A data.frame: 4 × 2
24	120
45	3000
67	600
88	500
```

```R
dataset2 <- shopping_data %>%
select(product,price)%>%
filter(price>45)%>%
group_by( product)%>%
summarize(avg = mean(price))

dataset2 
```

Output is,

```R
A tibble: 6 × 2
noodle	90
orange	67
papaya	88
pee	89
Rice	56
wheat	78
```

### Arrange function

It sort our dataframe in acending order.
`arrange(price)`, to arrange dataframe in decending order we used `arrange(desc(price))`
```R
arrange(product,price)
```

```R
Output is,
A data.frame: 8 × 2
24	120
45	3000
56	45
67	600
78	67
88	500
89	89
90	90
```

# Managing control statements:

* If statement:

If statement is the most common statement that execute code that only the condition place between bracket is true. Otherwise if statement ignore that particular piece of code.
` if(condition){
code to be executed}`
 to overcome this abstacle we add extra element else
 # Paste function
Paste converts its arguments ( via as.character) to character strings and concatenates them (separating them by the string given by sep ). If the arguments are vectors, they are concatenated term-by-term to give a character vector result.
```R
product <- "tshirt"
price<- 110
if(price < 100){
    print(paste('adding',product,'to cart'))
}else
{
    print(paste('adding',product,'to wishlist'))
}
```
Output is,

```R
[1] "adding tshirt to wishlist"
```

# Control Statement in vectors

```R
quantity <- c(1,1,2,3,4)
ifelse(quantity == 1,'Yes','No')
```

Output is,

```R
'Yes''Yes''No''No''No'
```

```R
price <- 100
if(price < 100){
    print("price"< "budget")
}else if(price == 100){
    print("the price is equal to budget")
    
}else{
    print("The budget is less then price")
}
```

Output is,

```R
[1] "the price is equal to budget"
```

```R
price <- c(58,100,110)
if(price < 100){
    print("price"< "budget")
}else if(price == 100){
    print("the price is equal to budget")
    
}else{
    print("The budget is less then price")
}
```

If the condition has the lenght grater than one then only the first input is tested. That means it check the first elements and then stop. This problem is resolved by using any function.

#  Any Function

```R
if(any(price < 100)){
    
    print('At least one price is under budget')
}
```

Output is,

```R
[1] "At least one price is under budget"
```

# All Function

```R
if(all(price<100)){
    print('all the price are under budget')
}else{
    print('Not all prices satisfies the condition.')
}
```

Output is,

```R
[1] "Not all prices satisfies the condition."
```

To combine the condition we can use `&&` and `||` operator. single and and or are used to element wise vector. While double and or are used for vector compare on one(non vectorise form)

```R
price <- 58
if(price> 50 && price < 100){
    print('The price is between 50 and 100')
}else {
    print("the price is not in between 50 and 100")
}
```

```R
[1] "The price is between 50 and 100"
```

# Switch Statement

We can add as many as if else statements however keeping more than four is difficult to keep track what is happing when the condition is true. The switch command work with the cases, each syntax contain value to be tested followed by the possible cases.

```R
quantity <- c(1,3,4,5)

average_quantity <- function(quantity,type) {
    switch(type,
          arthematic = mean(quantity),
          geometric = prod(quantity)^(1/length(quantity)))
}
average_quantity(quantity,"arthematic")
```

Output is,

```R
3.25
```

```R
x <- c(1,2,3,4,5)
sumfunction <- function(x,i){
    switch(i, 
          s = sum(x)
        )
}
sumfunction(x,"s")
```

Output is,

```R
15
```

# Loop
Loop is the sequence of instructions that are repeated untill a certain condition is reached.
* For loop
It perform the same operations on all elements from input.
Its syntax is `if(variable in sequence ){ Expression}`
between parenthesis there are three argument first argument is variable which can take any name then we have keyword in and last is sequence or vector of any kind.

For loop does not save output untill we print it.
```R
cart <- c('apple','cookie','lemoan')
    for(product in cart){
        print(product)
    }
```
Output is,
```R
[1] "apple"
[1] "cookie"
[1] "lemoan"
```
# While loop
While loop perform the operation as long as given conditions is true. Syntax is similary as for loop. To make loop stop there must be relation between condtion and expression other wise loop does not stop ever.
```R
index <- 1
while(index <3 ) {
    print(paste("The index value is",index))
    index <- index + 1
}
```
Output is, 

```R
[1] "The index value is 1"
[1] "The index value is 2"
```
# Repeat Loop
They repeat the same operation untill it hitting the stop key or by inserting special function to stop them. Repeat loop are important in algorithms optimization and maximization. As an syntax `repeat expression`

The next statement is used to discontinue one particular cycle and skip to the next.

```R
x <- 1
repeat {
    print(x)
    x = x + 1
    if( x==3){
        break
    }
}
```
Output is,
```R
[1] 1
[1] 2
```
```R
price <- c(123,456,78,900,987)
for(value in price){
    if( value < 100){
        next
    }
    discount <- value - value * 0.1
    print(discount)
}
```
Output is,
```R
[1] 110.7
[1] 410.4
[1] 810
[1] 888.3
```


 



