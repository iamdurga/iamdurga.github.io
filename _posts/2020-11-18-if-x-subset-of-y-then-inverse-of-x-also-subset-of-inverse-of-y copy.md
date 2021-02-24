---
title:  "If x Subset Of Y Then Inverse Of x Also Subset Of Y?"
date:   2020-11-18 01:29:17 +0545
categories: Measure-theory
tags:
  - Range
  - Domain
header:
  teaser: "assets/header_images/1.png"
  overlay_image: "assets/header_images/6.png"
---

Let
$$ f : X \rightarrow Y $$ be a function. If  B is subset of  y then its inverse image $$ f^-B $$ is the subset of  x define by 

$$ f^-B = {x : f(x) \in B} $$ 

Now prove the following.
 
$$
i. B_1 \subset B_2 \Rightarrow f^-B_1  \subset f^- B_1 
$$

$$  
ii. f^-\cup_i B_i = \cup_i f^-B_i 
$$ 

$$ 
iii. f^-\cap_i B_i \subset \cap_i f^-B_i
$$
    
Solution: 

Let 
$$ F(x) : x \rightarrow y $$

be a function. If B is the subset of Y, then it's inverse maps 
$$ f^-x $$
is the subset of x define by 

$$ f^-B = { f(x) \in B} $$

i. 

$$
let\ x \in f^-B_1\ then\ f(x) \in B_1 
$$

$$
since\  B_1 \subset B_1 
$$

$$ we\ can\ write\ \\  
f(x) \in f^-(B_2)
$$

ii.

$$ Suppose\ ,  x \in f^-\cup_i(B_i) $$

$$ f(X) \in \cup_i(B_i) $$

$$ So\ f(x) \in B_i for\ some\ i $$ 

this implies that, 

$$ x \in f^-B_i $$

$$ So\ x \in \cap_i f^-(B_i)$$

Conversely 

$$ Suppose\ x \in \cap_i f^-(B_i) $$

$$ Then\  x \in f^-(B_i)\ for\ some\ i   $$
  
$$
So\ f(x) \in B_i \subset (\cap_iB_i) 
$$ 
 
therefore

$$ f(x) \in (\cap_i B_i) $$

and hence

$$ x \in f^-(\cap_iB_i)$$




