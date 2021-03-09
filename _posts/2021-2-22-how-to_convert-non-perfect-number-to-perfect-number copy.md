---
title:  "How To Convert Non Perfect Number Into Perfect Number Using Python?"
date:   2021-2-22 01:29:17 +0545
categories: Python-Biginner
tags:
  - Number-system
  - Biginner
header:
  teaser: "assets/header_images/7.png"
  overlay_image: "assets/header_images/3.png"
---
# Conversion From Non Perfect Number Into Perfect Number.

## Introduction
As we have studied in our early school days, a perfect number is a number that is a square of another number. Also, we can define a perfect number as a product with the same number or product of two equal numbers. For example, 25 is a perfect number because it is the product of two 5. Perfect numbers are always positive. We have many formulae for the perfect number we are using these formulae since school. 

My goal here is to tried to write basic python code to the non perfect numbers how can we change it to the perfect number. 


## How to do it ? 
As our basic concept is applying while loop and find out nearest perfect number from our number and how much we need to add or substract to change perfect number. 

## In Python 



Creation of python program to convert a non-perfect number into the perfect number.
For this take a number as an input and apply the general formula which we used to check whether it is a perfect square or not at the school level. If our given number is already perfect we do not need to go further process. If our given number is not perfect we initialize `before` as 0 `after` as 1 and `curr_num` as 1. Now we start while loop and again used the formula which is used to check perfect square or not in the integer type. If croot's square equal to the current number we do not need to go for the internal loop. If that not we compare our given number with `curr-num` if our number is less than `curr_num` we change before equal `curr_num` if the number is greater than `curr_num` we change `after` which is equal to current. In each iteration our `curr_num` increases by 1, the rest of the code is given below.

```python
n = int(input('Enter an integer'))
root = int(n**0.5)

if root** 2 == n:
    print('Your number is already perfect.')
else:
    before = 0
    after = 1
    curr_num = 1
    while True:
        croot = int(curr_num**0.5)
        if croot** 2 == curr_num:
            if curr_num < n:
                before = curr_num
            else:
                after = curr_num
        #print(curr_num,before,after)
        if after != 1:
            if n - before < after - n:
                print(f'perfect number around{n} are {before} and {after}')
                print(f'your nearest perfect number around {n} is {before}')
                print(f'we have to subtract {n - before} to make {n} perfect number.')
            else:
                print(f'perfect number around {n}  are {before} and { after }')
                print(f'your nearest perfect number around {n} is { after}')
                print(f'we have to add {after - n} to make {n} perfect number.')
                break
        curr_num += 1
```
