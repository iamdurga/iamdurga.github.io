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
As we all know about square numbers, in mathematics, a square number or perfect square number is a number that is the product of a number with itself. For example, 4 * 4 = 16, 2 * 2 = 4, and 6 * 6 = 36.

My goal here is to try to write basic Python code to solve the grade 4 problem. 


## How to do it ? 
My basic concept here is to provide numbers in the specified range and initialize an empty list to store the results. I then applied the appropriate condition.

## In Python
My basic concept here is to generate numbers in the range from 1 to 101 to find the square numbers between 1 and 100. As we know, in a range, the lower point is inclusive and the upper point is exclusive, so I used the range from 1 to 101. I created an empty list to store the square numbers and applied a for loop. I defined a variable `root` as the square root of the iteration variable. Then, I rounded `root` using the `round()` function, which returns a floating-point number rounded to the specified number of decimals. Next, I applied the condition that if the square of the rounded `root` is equal to the iteration variable `n`, then that iteration variable is a perfect square number, and it is added to the `root_numbers` list. This process is applied for all iteration variables until the last iteration variable, which is 100.

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
