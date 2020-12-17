---
title:  "How To Convert Decimal To Binary In Python?"
date:   2020-12-15 01:29:17 +0545
categories: Python-Programming-Language
tags:
  - Initialize
  - Loop
header:
  teaser: "assets/header_images/8.png"
  overlay_image: "assets/header_images/6.png"
---
## Conversion From Decimal to Binary in python.

Creation of python program to convert decimal to binary.
For this take decimal number as input. Initialize current decimal as given decimal. Initialize remender as zero. Create a place to store binary number. We don't know about how many step are taken to convert so I choosed while loop. If current decimal is divisiable by 2 then remender is zero. Now I took current decimal  as quotient of original decimal number. I kept remender in place where I create the place to store it. Else I kept remender 1 in list. Similar process I repeat below. 


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

print(binary)

binary = binary[::-1]

print(binary)
