---
title:  "How To Find Multiple Numbers of 3 or 5 or Any Numbers from given range Using Python Dictionary?"
date:   2021-3-18 01:29:17 +0545
categories: Python-Beginner
tags:
  - Multiple-Numbers
  - Beginner
header:
  teaser: "assets/header_images/2.png"
  overlay_image: "assets/header_images/5.png"
---
# How to findout multiple numbers.

## Introduction
As we all familiar with multiplication tables up to 9. If we knew the multiplication table then we can able find multiple numbers of any number. For example multiple numbers of 3 up to 100 are: 3, 6, 9, 12, 15, 18, 21, 24, 27, 30, 33, 36, 39, 42, 45, 48​, 51, 54, 57, 60, 63, 66, 69, 72, 75, 78, 81, 84, 87, 90, 93, 96, 99. Similarly, we can find any numbers.  

My goal here is to try to write basic Python code to solve the grade 3 problem. 


## How to do it ? 
My basic concept here is I create an empty dictionary to store the result. In the dictionary, I kept numbers as a key and multiple numbers as a value. I run for loop in a specified range and applied the required condition to find out required number's multiple numbers.
## In Python
In python, at first, I create an empty dictionary. I initialize range from 1 to 99 which I kept in a list as a `numbers`. I also initialize `Multiple_of_3` and `Multiple_of_5` as an empty list to store the required multiple numbers. I apply for a loop in a specified range. If given numbers(iteration variable) n is divisible by 3 then the numbers go to the `Multiple_of_3` list also if given numbers(iteration variable) n is divisible by 5 then the numbers go to the `Multiple_of_5` list. Finally, I store `Multiple_of_3` and `Multiple_of_5` as a key and required multiple numbers as value. And my python code is given below.

```python
my_dict = {}
numbers = list(range(1,99))
Multiple_of_3 = []
Multiple_of_5 = []
for n in numbers:
    if n %3 == 0:
        Multiple_of_3.append(n)
    if n% 5 == 0:
        Multiple_of_5.append(n)
        
my_dict['Multiple_of_3'] = Multiple_of_3
my_dict['Multiple_of_5']= Multiple_of_5
print(my_dict)
```
Output of the above code is
```
{'Multiple_of_3': [3, 6, 9, 12, 15, 18, 21, 24, 27, 30, 33, 36, 39, 42, 45, 48, 51, 54, 57, 60, 63, 66, 69, 72, 75, 78, 81, 84, 87, 90, 93, 96], 'Multiple_of_5': [5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55, 60, 65, 70, 75, 80, 85, 90, 95]}

```
