---
title:  "How To Find Composite And Prime Using Python?"
date:   2021-2-26 01:29:17 +0545
categories: Python-Beginner
tags:
  - prime-composite
  - Beginner
header:
  teaser: "assets/header_images/6.png"
  overlay_image: "assets/header_images/8.png"
---
# How to findout prime or composite.

## Introduction
As we are all familiar with prime and composite numbers from earlier days, a prime number is simply a number that has factors of 1 and itself. Similarly, a composite number is a number that has more than two factors. However, 1 is neither a prime number nor a composite number. 13 is a prime number because the only possible factors of 13 are 1 and 13, but 12 is a composite number because its factors are 1, 2, 3, 4, 6, and 12.  

My goal here is to tried to write basic python code to solve grade 4 problem . 


## How to do it ? 
My basic concept is I make a function name as prime or composite which take a testing number, if we call function then we can get desire result. 

## In Python
Here I tried to write a function named `prime_or_composite`, which takes \( n \) as the testing number. Initialize factors as zero. We apply a for loop from the range 1 to \( \frac{number}{2} + 1 \). We check if the given number is divisible by the iteration variable. If the iteration variable divides the number and the count of factors is greater than 2, then it prints that the number is composite; otherwise, it prints that the number is prime.

```python
def prime_or_composite(n):
    f = 0
    for i in range(1,int(n/2)+1):
        if n % i == 0:
            f += 1
            
    if f >= 2:
        print(f"{n} is composite.")
    else:
        print(f"{n} is prime.")
prime_or_composite(6)
```
Output of the above code is
```
6 is composite.
```
