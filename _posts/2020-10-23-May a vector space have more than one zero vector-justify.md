---
title:  "May a vector space have more than one zero vector?justify"
date:   2020-10-23 01:29:17 +0545
categories: Linear Algebra
tags:
  - Vectorspace
  - Basis
header:
  teaser: "assets/head.png"
  overlay_image: "assets/images/what-if.png"
---        
**Question:** May a vector space have more than one zero vector?justify. Let $$v = {(a_1, a_2):a_1, a_2 \in R} $$. for $$ (a_1, a_2) $$ , $$ (b_1, b_2) $$ = $$ (a_1 + 2b_1,  a_2 + 3b_2) $$ and $$ c(a_1, a_2) $$ = $$ (ca_1, a_2)$$ .Is v a vector space over f with these operations? justify your answer.

Solution:\
Let a vector space have two zeros say 0 and 0^'. From $v_{s3}$  0 is the identity  under addition\
Hence $$ \forall  x \in V $$\
             x + 0 = 0 + x = x............(1)\
             also from $v_{s3}$   0' is identity under addition.\
             x + 0' = 0' + x = x..........(2)\
            From (1) and (2)\
            x + 0 = x + $$ 0' $$  = x .\
            Hence there is unique zeros in vector space.
            
**Second part**

Here given\
v = $${(a_1, a_2):a_1, a_2 \in R}$$ for $$(a_1, a_2),\ (b_1, b_2) \in V$$ and $$c \in R $$ \
Define $$(a_1, a_2) + (b_1 , b_2) = (a_1 + 2b_1,  a_2 + 3b_2)$$ and $$ c(a_1, a_2)  =  (ca_1, a_2) $$
$$V_{s1}:$$ for $$(a_1, a_2), (b_1, b_2) \in V $$
$$(a_1, a_2) + (b_1, b_2)  =  (a_1 + 2a_2, b_1 + 3b_2) \neq (a_2 + 2a_1, b_2 + 3b_1) \neq (b_1, b_2) + (a_1, a_2)$$\
$$V_{s1}$$ does not hold.\
$$V_{s2}$$: for $$(a_1, a_2), (b_1, b_2) \in V\ and\ (c_1, c_2) \in V $$\
$$[(a_1, a_2) + (b_1, b_2)] + (c_1, c_2)  = [ a_1 + 2b_1, a_2 + 3b_2] + (c_1, c_2) \neq $$ 
$$(a_1 + 2b_1 + c_1,  a_2 + 3b_2 + 3b_3) \neq (a_1, a_2) + [ b_1 + 2c_1, b_2 + 3c_2] \neq (a_1, b_2) + [(b_1, b_2) + (c_1, c_2)]$$\
$$V_{s2}$$ does not hold.

$$V_{s3}$$:if there exist a element  z = $$(d_1, d_2) \in V$$ such that $$(a_1, a_2) + (d_1, d_2) =(a_1, a_2)$$\
$$(a_1 + 2d_1, a_2 + 3d_2) = (a_1, a_2)$$\
$$a_1 + 2d_1  = a_1 \Rightarrow d_1 = 0$$\
$$a_2 + 3d_2  = a_2 \Rightarrow d_2 = 0$$\
This show that $$(a_1, a_2) + (0, 0) = (a_1, a_2)$$

$$v_{s4}$$:Let $$\forall  (a_1, b_1) \exists (-a_1, -a_2) \in V$$ 
such that $$ (a_1, a_2) + (-a_1, -a_2) = [a_1 +(-2a_1), a_2 + (-3a_2)] = (-a_1, -2a_2) \neq (0, 0)$$.\
Hence $$ v_{s4}$$ does not satisfy.

$$V_{s5}: 1 \in  F\ 1.(a_1, b_1) = (1.a_1, b_1) = (a_1, b_1)$$\
$$V_{s6}: \forall x, y \in F\ xy(a_1, b_1) = x(ya_1, b) = x[y(a_1, b1)]$$\
$$V_{s7}: \forall x, y \in F\ (x+y) (a_1, b_1)  = [(x+y)a_1, b_1] = (xa_1  + ya_1, b_1)$$\
also $$x(a_1, b_1) + y(a_1, b_2) = (xa_1, b_1) + (ya_1, b_1)  = (xa_1 + ya_1, b_1 + b_2) = (xa_1 + ya_1, 2b_1)$$\
$$(x+y)(a_1, b_1) ≠ x(a_1, b_1) + y(a_1, b_1)$$\
Hence $$v_{s7}$$ does not satisfy.

$$V_{s8}$$: $$\forall  x \in F$$  $$ x[(a_1, b_1) + (a_2, b_2)]  = x(a_1, b_1) + x(a_2, b_2) $$ = $$(xa_1, b_1) + (xa_2, b_2)$$\
All the condition of vector space does not satisfy hence it is not vector space.
