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
As we have studied in our early school days, decimal is a number system with base 10, which means that we will have 10 numbers sequentially starting from zero. The binary system is a number system with a base of two, which means that we have to represent every number with 0 and 1. Similarly, in the octal system, the highest possible digit is 7. In the binary system, we have two digits, and according to set theory, the number of arrangements that can be made with n digits is \( 2^n \) (each arrangement must be of length n), so we will have 4 possible numbers in the binary system of length two.

My target here is to learn basic Python by trying to solve my grade 7 homework.


## How to do it ? 
As per our basic concept of collecting remainders from a number after dividing by 2, we have to stop dividing the quotient after we reach 1.

## In Python 



Creation of a Python program to convert decimal to binary.
For this, take the decimal number as input. Initialize the current decimal as the given decimal. Initialize the remainder as zero. Create a place to store the binary number. We don't know how many steps are taken to convert, so I chose a while loop. If the current decimal is divisible by 2, then the remainder is zero. Now, I took the current decimal as the quotient of the original decimal number. I kept the remainder in the place where I created the place to store it. Else, I kept the remainder 1 in the list. I repeat a similar process below. 

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
