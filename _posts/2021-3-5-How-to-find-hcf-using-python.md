---
title:  "How To Find HCF Using Python?"
date:   2021-3-5 01:29:17 +0545
categories: Python-Beginner
tags:
  - HCF
  - Beginner
header:
  teaser: "assets/header_images/1.png"
  overlay_image: "assets/header_images/5.png"
---
# How to findout HCF.

## Introduction
As we all know, HCF stands for Highest Common Factor. The definition of HCF is the highest common factor that divides two or more numbers. It is one method of solving problems in early school classes. For example, the HCF of 12 and 6 is 6. Similarly, the HCF of 4, 8, and 10 is 2 because 2 is the highest factor common to 4, 8, and 10.

My goal here is to try to write basic Python code to solve the grade 5 problem. 


## How to do it ? 
My basic concept is I make a function name as HCF  which take two testing number, if we call function then we can get desire result. 

## In Python
Here, I tried to write a function named `HCF` that takes \( n1 \) and \( n2 \) as input numbers. Initialize the variable \( m1 \) as the minimum of the two numbers and \( m2 \) as the maximum of the two numbers \( n1 \) and \( n2 \). The variable \( CF \) stores the common factors as a list. We apply a for loop from the range 1 to the minimum number + 1 because the range includes the starting number but excludes the end number. I took the range up to the minimum number because the greatest common factor would only be the minimum number. We check if our iteration variable in the range divides both the maximum number and the minimum number. Among these iteration variables, the greatest iteration variable that divides both \( m1 \) and \( m2 \) is the HCF. The function then returns the desired output.

```python
def HCF(n1,n2):
    m1 = min(n1,n2)
    m2 = max(n1,n2)
    CF = []
    for i in range(1,m1+1):
        if m1 % i == 0 and m2 % i == 0:
            CF.append(i)
    print(f"Common factor of {n1} and {n2} are {CF}.")
    print(f"HCF of {n1} and {n2} is {max(CF)}.")
HCF(4,8)
```
Output of the above code is
```
Common factor of 4 and 8 are [1, 2, 4].
HCF of 4 and 8 is 4.

```
