---
title:  "How To Find Composit And Prime Using Python?"
date:   2021-2-26 01:29:17 +0545
categories: Python-Biginner
tags:
  - prime-composit
  - Biginner
header:
  teaser: "assets/header_images/6.png"
  overlay_image: "assets/header_images8.png"
---
# How to findout prime or composit.

## Introduction
As we all familiar about prime and composit number from earlier days. Simply prime number is that number which has factor as 1 and itself. Similarly composit number is a number which has more than two factors. However 1 is neither prime number nor composit number. 13 is prime number because possible factors of 13 are only 1 and 13, but 12 is prime number due to factors of 12 are 1,2,3,4,6,12.  

My goal here is to tried to write basic python code to solve grade 4 problem . 


## How to do it ? 
My basic concept is I make a function name as prime or composit which take a testing number, if we call function then we can get desire result. 

## In Python
Here I tried to write a function that has the name `prime_or_composit` which can take n as a testing number. Initialize factors as zero. We apply for loop from range 1 to number divided by 2 + 1 times. We checked if a given number is divisible by the iteration variable. If the iteration variable divides the number and is greater than 2 then it prints that number as composite otherwise prints number as prime. 

```python
def prime_or_composit(n):
    f = 0
    for i in range(1,int(n/2)+1):
        if n % i == 0:
            f += 1
            
    if f >= 2:
        print(f"{n} is composit.")
    else:
        print(f"{n} is prime.")
prime_or_composit(6)
```
Output of the above code is
```
6 is composit.
```
