---
title:  "Is Complex Fourier Is Same With Real Fourier?"
date:   2020-11-30 01:29:17 +0545
categories: Differential-Equation
tags:
  - Even
  - Odd
header:
  teaser: "assets/header_images/5.png"
  overlay_image: "assets/header_images/6.png"
---
# Complex form of fourier series

The complex form of fourier series is obtained by exaprassiong 
$$ cos\frac{n\pi.x}{l}$$ and $$ sin\frac{n\pi.x}{l} $$ in expontial form that is,
$$
f(x) = \frac{a_0}{2} + \sum_{i=1}^\infty[a_ncos\frac{n.\pi.x}{l}+b_nsin\frac{n.\pi.x}{l}]\\
f(x) = \frac{a_0}{2} + \sum_{i=1}^\infty[\frac{\epsilon^(\frac{n.\pi.x}{l}+\epsilon^(\frac{-n.\pi.x}{l}}{2}]a_n+ \sum_{i=1}^\infty[\frac{\epsilon^(\frac{n.\pi.x}{l}-\epsilon^(\frac{-n.\pi.x}{l}}{2i}]b_n 
$$

# Even Odd function:-

In simple we know that function is even if 

$$ f(-x) = f(x) $$.

and function is odd if 

$$ f(-x) = -f(x) $$.

example of even is cos function and example of odd functio is sin function.The fourier coeffient $$ b_n $$ zero it have value for 
$$ a_0 $$ and $$ a_n $$ is odd and fourier cofficent $$ a_0 $$ and 
$$ a_n $$ zero have value for $$ b_n $$ is even.