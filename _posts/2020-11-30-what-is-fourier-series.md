---
title:  "What Is Fourier Series?"
date:   2020-11-30 01:29:17 +0545
categories: Differential Equation
tags:
  - Even
  - Odd
header:
  teaser: "assets/header_images/6.png"
  overlay_image: "assets/header_images/8.png"
---
# What is fourior Series 

It is the method of expressing any given function in terms of sine and cosine series. The Fourier theorem's can be expressed as " any single valued function defined in the interval $$ [\pi,\pi] $$ may be represented over this interval by trigonometric series.

$$
f(x) = \frac{a_0}{2} + \sum_{i=1}^\infty[a_ncos(nx) + b_nsin(nx)]
$$

Where

$$ a_0, a_n , b_n $$  are called fourier coefficent, and  $$ a_0, a_n, b_n $$

are determined by the following formula,

$$
1.\ a_0 = \frac{1}{\pi}\int_{-\pi}^\pi f(x) dx. \\

2.\ a_n = \frac{1}{\pi}\int_{-\pi}^\pi f(x)cos(nx) dx. \\

3.\ b_n = \frac{1}{\pi}\int_{-\pi}^\pi f(x)sin(nx) dx.\\ 
$$

Where  n = 1, 2, 3, .....

## Fourier series expression for any arbitrary function in various interval

Thus far, the expansion interval has been restricted to $$ [\pi , \pi]$$. To solve many physical problems, it is necessary to develop a fourier series that will be valid over a wide interval.

*  Fourire series in [a , b]

If f(x) is periodic in interval [a , b] 

i;e $$ f(x + a + b) = f(x) $$ 

the fourier series expansion of f(x) is,

$$

f(x) = \frac{a_0}{2} + \sum_{i=1}^\infty[a_ncos\frac{2n.\pi.x}{b-a}+b_nsin\frac{2n.\pi.x}{b-a}] \\

where\\

a_0 = \frac{1}{b-a}\int_{a}^b f(x) dx.\\

a_n = \frac{1}{b-a}\int_{a}^b f(x)cos\frac{2n.\pi.x}{b-a} dx.\\

b_n = \frac{1}{b-a}\int_{a}^b f(x)sin\frac{2n.\pi.x}{b-a}. \\

$$ 


* Fourier series in [-l , l]

Similarly the function f(x) is periodic in the interval [-l , l] 

i;e 

$$ f(x + 2l) = f(x) $$

the fourior series expansion of f(x) is,

$$
f(x) = \frac{a_0}{2} + \sum_{i=1}^\infty[a_ncos\frac{2n.\pi.x}{l+l}+b_nsin\frac{2n.\pi.x}{l+l}] \\

where\\

a_0 = \frac{1}{l}\int_{-l}^l f(x) dx.\\

a_n = \frac{1}{l}\int_{-l}^l f(x)cos\frac{n.\pi.n}{l} dx.\\

b_n = \frac{1}{l}\int_{-l}^l f(x)sin\frac{n.\pi.n}{l} dx.\\

$$