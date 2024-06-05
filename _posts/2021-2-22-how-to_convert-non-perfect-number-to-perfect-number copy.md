---
title:  "How To Convert Non Perfect Number Into Perfect Number Using Python?"
date:   2021-2-22 01:29:17 +0545
categories: Python-Beginner
tags:
  - Number-system
  - Beginner
header:
  teaser: "assets/header_images/7.png"
  overlay_image: "assets/header_images/3.png"
---
# Conversion From Non Perfect Number Into Perfect Number.

## Introduction
As we studied in our early school days, a perfect number is a number that is a square of another number. Also, we can define a perfect number as a product of the same number or the product of two equal numbers. For example, 25 is a perfect number because it is the product of two 5s. Perfect numbers are always positive. We have many formulas for perfect numbers, and we have been using these formulas since school.

My goal here is to try to write basic Python code to convert non-perfect numbers into perfect numbers. 


## How to do it ? 
As our basic concept is to apply a while loop to find the nearest perfect number from our number and determine how much we need to add or subtract to reach the perfect number.

## In Python 

Creation of a Python program to convert a non-perfect number into a perfect number:

To do this, take a number as input and apply the general formula used to check whether it is a perfect square, as learned in school. If our given number is already perfect, we do not need to proceed further. If our given number is not perfect, we initialize `before` as 0, `after` as 1, and `curr_num` as 1. 

Now we start a while loop and use the formula again to check if the current number is a perfect square in integer form. If the square of the cube root equals the current number, we do not need to go further in the loop. If not, we compare our given number with `curr_num`. If our number is less than `curr_num`, we set `before` equal to `curr_num`. If the number is greater than `curr_num`, we set `after` equal to the current number. In each iteration, our `curr_num` increases by 1. The rest of the code is given below.

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
