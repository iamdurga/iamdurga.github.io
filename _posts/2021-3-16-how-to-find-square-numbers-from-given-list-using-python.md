---
title:  "How To Find Square Numbers From Given List Using Python?"
date:   2021-3-16 01:29:17 +0545
categories: Python-Beginner
tags:
  - Square-Number
  - Beginner
header:
  teaser: "assets/header_images/4.png"
  overlay_image: "assets/header_images/7.png"
---
# How to findout Square Number.

## Introduction
As we all knew about square number. In mathematics square number or perfect square number is a number which is product of number with itself. For example 4 * 4 = 16, 2 * 2 = 4, 6 * 6 = 36.  

My goal here is to try to write basic Python code to solve the grade 4 problem. 


## How to do it ? 
My basic concept is here I gave numbers in the specified numbers of range and initialize empty list to store the result. And applied appropirate condition. 

## In Python
My basic concept is here I gave numbers in the range 1 to 101 to find the square numbers between 1 to 100. We already had known that in a range lower point is inclusive and the upper point is exclusive. so, here I took range 1 to 101. I made an empty list to store the square numbers. And I applied for a loop. And I define root which is given iteration variable's power one upon two. I round the int_root. Usage​​ of round() function is which returns a floating-point number that is a rounded version of the specified number, with the specified number of decimals. And I applied the condition if int_root's power 2 is equal to n then that an iteration variable is a perfect number and it goes to the `root_numbers` list. A similar process is applied for all of the iteration variables until the last iteration variable is 100. 

```python
numbers = list(range(1,101))
root_numbers = []
for n in numbers:
    root = (n)**0.5
    int_root = round(root)
    if int_root**2 == n:
        root_numbers.append(n)
        print(n)
```
Output of the above code is
```
1
4
9
16
25
36
49
64
81
100

```
