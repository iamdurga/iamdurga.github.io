---
title:  "How To Convert Decimal To Binary In Python?"
date:   2020-12-15 01:29:17 +0545
categories: Python-Beginner
tags:
  - Number-system
  - Beginner
header:
  teaser: "assets/header_images/8.png"
  overlay_image: "assets/header_images/6.png"
---
# Conversion From Decimal to Binary in Python.

## Introduction
As we have studied in our early school days, decimal is a number system with base 10 which means that we will have 10 numbers sequentially starting from zero. Binary system is a number system with a base of two which means that we have to represent every number with 0 and 1. Simillary in octal system highest possible digit is 7. In binary system, we have two digits and according to set theory, number of arrangements that can be made with n digits is $$ 2^n $$ (each arrangement must be a length n) so we will have 4 possible numbers in binary system of length two. 

My target here is to learn basic python by trying to solve my grade 7 homework. 


## How to do it ? 
As our basic concept of collecting remainders from a number after dividing by 2, we have to stop dividing quotient after we reached 1. 

## In Python 



Creation of python program to convert decimal to binary.
For this take decimal number as input. Initialize current decimal as given decimal. Initialize remender as zero. Create a place to store binary number. We don't know about how many step are taken to convert so I choosed while loop. If current decimal is divisiable by 2 then remender is zero. Now I took current decimal  as quotient of original decimal number. I kept remender in place where I create the place to store it. Else I kept remender 1 in list. Similar process I repeat below. 

```python 

dec = int(input("Enter a decimal number. "))
curr_dec = dec
rem = 0
binary = []
while True:
    if curr_dec % 2 == 0:
        rem = 0
        curr_dec = int(curr_dec/2)
        binary.append(rem)
    else:
        rem = 1
        curr_dec = int(curr_dec/2)
        binary.append(rem)
    if curr_dec  == 1:
        binary.append(1)
        break
#print(binary)
binary = binary[::-1]
x = [str(i) for i in x]
x = "".join(x)
print(x) 
```
