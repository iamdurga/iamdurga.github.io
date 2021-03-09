---
title:  "How To Find HCF Using Python?"
date:   2021-3-5 01:29:17 +0545
categories: Python-Biginner
tags:
  - HCF
  - Biginner
header:
  teaser: "assets/header_images/1.png"
  overlay_image: "assets/header_images4.png"
---
# How to findout HCF.

## Introduction
As we all knew HCF. It stands for Highest Common Factor. Definition of HCF is the highest common factor which divides both of two or more numbers is called the highest common factor. It is one method of solving the problem in the earlier school class. For example, the HCF of 12 and 6 is 6. Similarly, HCF of 4, 8, 10 is 2 because 2 is the highest of factors of 4, 8, 10.  

My goal here is to try to write basic Python code to solve the grade 5 problem. 


## How to do it ? 
My basic concept is I make a function name as HCF  which take two testing number, if we call function then we can get desire result. 

## In Python
Here I tried to write a function that has the name `HCF` which can take n1 and n2 as a testing number. Initialize variable m1 as the minimum of two numbers and m2 as the maximum of two numbers n1 and n2 and CF store the common factor as a list. We apply for a loop from range 1 to a minimum of number + 1 because the range includes starting number but excludes the end number. Here I took range up to minimum among them because the greatest common factor would be an only minimum number. We checked if our iteration variable lies in the range that divides both maximum number and minimum. Among these iteration variables, the greatest iteration variable which divided both m1 and m2 is HCF. And return the desired output. 

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
