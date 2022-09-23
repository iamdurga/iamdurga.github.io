---
title:  "How to calculate integration using Monte Carlo Method?"
date:   2022-09-15 09:29:17 +0545
categories: Monte Carlo Simulation
tags:
  - Random Number
  - Random Number Generation
  - Congruential Method
header:
  teaser: "assets/monte/output_5_0.png"
  overlay_image: "assets/monte/output_5_0.png"
toc: true
---
# Introduction integration 

In mathematics, an integral assigns numbers to functions in a way that describes displacement, area, volume, and other concepts that arise by combining infinitesimal data. The process of finding integrals is called integration [source](https://en.wikipedia.org/wiki/Integral). To solve the many Data Science problem we should use integration. In Data Science we need to use not only singal dimensional integral, hence there is requirement of used of multi dimensional integration to solve many Data Science problem. 

In this blog we are going to introduce integration of complex function using Monte Carlo method and later we estimate the error of our calculated integration.

Lets us consider following integration problem,

![image]({{site.url}}/assets/monte/1.png)


 If we solve this problem mathematically we get, 

![image]({{site.url}}/assets/monte/2.png)

Hence, actual value of above integration problem is 1.718281...


# Lets Calculate it's value using Monte Carlo Method 

### Algorithm
1. impost random number
2. Choose N(i.e no of MC steps)
3. Perform a loop over N such that you choose $x_i \in (0,1)$.
4. Find f(xi)
5. find mean
6. print


```python
import random
import math
import numpy as np 
import matplotlib.pyplot as plt
```


```python
print("True Mean:")
true_value = 1.718281828459045
N = [100,1000,10000,100000,100000,1000000]
d = {}
E = []
for i in range(len(N)):
    integral = 0 
    
    for j in range(N[i]):
        
        x = random.random()
        integral += np.exp(x)
    test_value = integral/j
    error = abs(test_value - true_value)
    E.append(error)
    print(f"Calculates Mean: {test_value}")
    print(f"Error Value of Mean: {error}")
    
    
```

    True Mean:
    Calculates Mean: 1.7533929772780017
    Error Value of Mean: 0.035111148818956606
    Calculates Mean: 1.7235132769915982
    Error Value of Mean: 0.005231448532553085
    Calculates Mean: 1.726876503411867
    Error Value of Mean: 0.008594674952821846
    Calculates Mean: 1.716686250054821
    Error Value of Mean: 0.001595578404224085
    Calculates Mean: 1.718391827316202
    Error Value of Mean: 0.00010999885715690105
    Calculates Mean: 1.7179675674235344
    Error Value of Mean: 0.00031426103551068785
    


```python
print(N, E)
```

    [100, 1000, 10000, 100000, 100000, 1000000] [0.035111148818956606, 0.005231448532553085, 0.008594674952821846, 0.001595578404224085, 0.00010999885715690105, 0.00031426103551068785]
    


```python
plt.plot(N, list(E))
plt.show()
```


    
![image]({{site.url}}/assets/monte/output_5_0.png)
    


As seen in the aforementioned image, when the number is originally tiny, the error value is high. Later on, as the number rises, the error value begins to fall.

# Lets Calculate Integration In the range [a,b)


```python

N = [100,1000,10000,100000]
for i in range(len(N)):
    a = 2
    b = 3
    integral = 0
    i = 0
    while N[i] < 1000:
        x = random.random()
        integral += math.exp(x)
        i = i + 1
        ans = integral * (b-a)/float(1000)
        print(ans)
```

    0.0014293209498465321
    0.0011720304229474166
    0.001912217584029893
    0.00213255359328241
    


```python

```
