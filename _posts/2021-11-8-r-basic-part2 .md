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
Dataframes are the most commonly used data structures in R. A dataframe is a list in which all components have names and are arranged in rows and columns. The easiest way to understand a dataframe is by visualizing it as a spreadsheet. The first row of a dataframe is typically represented as the header, and the header is defined by the names of the list components. Each column in a dataframe can store different data types, referred to as variables, and each row represents an observation across multiple variables.

Since dataframes resemble spreadsheets, data can be inserted in various ways to suit specific needs. There are multiple possibilities for data insertion.

| Product | apple | Banana|
|----------|-------|-------|
|price store A| 23 | 56|
| price store B | 67| 80|

This isn't a dataframe because the "price" data is divided into two parts. To transform this data into a dataframe, we would need to rearrange it by treating "product" as one variable, "price" as the next variable, and "store" as another variable. Once this rearrangement is done, it will become a dataframe.

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
By manipulating a dataframe, we can learn how to select, add new rows, and perform sorting and ranking operations within the dataframe. Dataframes are essentially lists where each element is a named vector of the same length. Consequently, we can select elements from dataframes much like we do with lists, using double square brackets `[[]]` or the `$` notation followed by the column name.

Furthermore, dataframes are also considered two-dimensional matrices. This means that we can index them as matrices using square brackets `[row, column]`. When we manipulate data in one dimension within dataframes, they behave like lists. Therefore, dataframes can be indexed either like lists or like matrices, depending on the positions, rules, and names involved.

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

During data analysis, a significant portion of our time is dedicated to data cleaning and transforming raw data. The tidyverse is an add-on that enables us to perform operations such as data cleaning and create powerful graphs, making the data analysis process more efficient and effective.

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

The `filter` function works similarly to the `select` function. By using the pipe operator `%>%`, we can chain multiple operations together at once without the need to rename intermediate results. This allows for a more streamlined and efficient data manipulation process.

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

To sort our dataframe in ascending order, we use the `arrange(price)` function. To arrange the dataframe in descending order, we use the `arrange(desc(price))` function.
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

The "if" statement is the most common statement used to execute code only if the condition placed between the brackets is true. Otherwise, the "if" statement ignores that particular piece of code.
` if(condition){
code to be executed}`
 to overcome this abstacle we add extra element else
 # Paste function
The "paste" function converts its arguments (via `as.character`) to character strings and concatenates them, separating them by the string given by "sep." If the arguments are vectors, they are concatenated term-by-term to produce a character vector result.
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

If the condition has a length greater than one, then only the first input is tested. This means it checks the first element and then stops. This problem can be resolved by using the "any" function.

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

To combine conditions, we can use the `&&` and `||` operators. Single `&` and `|` are used for element-wise vector operations, while double `&&` and `||` are used for non-vectorized forms of comparing vectors.

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

We can add as many `if` else statements as needed. However, keeping more than four can make it difficult to keep track of what is happening when the condition is true. The `switch` command works with cases, and each syntax contains a value to be tested followed by the possible cases.

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
It performs the same operation on all elements from the input. Its syntax is as follows: `if (variable in sequence) { Expression }`. Within the parentheses, there are three arguments: the first argument is a variable, which can have any name, followed by the keyword "in," and the last argument is a sequence or vector of any kind.

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
A `while` loop performs operations as long as the given condition is true. Its syntax is similar to that of a `for` loop. To make the loop stop, there must be a relation between the condition and the expression; otherwise, the loop will never stop.
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
Repeat loops repeat the same operation until they encounter a stop key or a special function that stops them. Repeat loops are important in algorithm optimization and maximization. Their syntax is as follows: `repeat { expression }`.

The `next` statement is used to discontinue one particular cycle and skip to the next one.

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


 



