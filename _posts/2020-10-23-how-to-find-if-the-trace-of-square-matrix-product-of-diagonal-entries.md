---
title:  "Is  The Trace of square matrix product of its diagonal element?"
date:   2020-10-23 01:29:17 +0545
categories: Linear-Algebra
tags:
  - Vectorspace
  - Basis
header:
  teaser: "assets/images/what-if.png"
  overlay_image: "assets/images/what-if.png"
---
**Question:** Is the trace of square matrice the product of its diagonal entries ? Justify. Determine whether the set $$w = [ (a_1 , a_2 , a_3) \in R_3 : a_1 + 2a_2 – 3a_3 = 2]$$ is subspace or not of $$ R^3$$ with justification.\

**Solution:**\
First part:\
No, the trace of square matrix is not the product of it's diagonal entries. The trace of a square matrix of order $$ m \times n $$ is the sum of its principal diagonal entries.\
i.e; Tr(M) = $$ M_{11} + M_{22} + M_{33} + .......+ M_{nn} $$\
Second part:\
			Here, $$ w =  [ (a_1 , a_2 , a_3) \in R^3 : a_1 + 2a_2 – 3a_3 = 2]$$. We have to show that w is  subspace of $$R^3$$\
			For this , we take $$(c_1 , c_2) \in R $$ and $$v_1 = (x_1 , x_2 , x_3)$$ and $$v_2 = (y_1 , y_2 , y_3) \in w$$\
			So, $$ x_1 + 2x_2 – 3x_3  = -2$$ ...............(i)\
			 $$  y_1 + 2y_2 – 3y_3  = -2$$...............(ii)\
			since,\
            $$ c_1v_1 + c_2v_2$$ \ 
			= $$ c_1(x_1 , x_2, x_3) + c_2(y_1 , y_2 , y_3)$$ \
 	 = $$(c_1x_1 + c_2y_1, c_1x_2 + c_2y_2 , c_1x_3 + c_2y_3)$$ \
                           Which is a traid form.\
                          By definition of w. \ 
                         $$ (c_1x_1 + c_2y_1) + 2(c_1x_2 + c_2y_2) – 3(c_1x_3 + c_2y_3)  = 2$$\
                        Or $$(c_1x_1 + 2c_1x_2 – 3c_1x_3 ) + (c_2y_1 + 2c_2y_2 – 3c_2y_3) = 2$$\
	Or $$ c_1(x_1 + 2x_2 – 3x_3 ) + c_2(y_1 + 2y_2 – 3y_3) = 2 $$\ 
	Or $$ 2c_1 + 2c_2 = 2 ≠ 0.c_1 + 0.c_2 = 0$$
	Or $$ c_1 + c_2 = 1$$.\
    Hence w is not subspace of $$R^3$$.\
    **Alternatively**\
    Given, $$ w =  [ (a_1 , a_2 , a_3) \in R^3 : a_1 + 2a_2 – 3a_3 = 2]$$.\
    If we choose\
    $$ u = (a_1, a_2, a_3) = (1, 2, 1) \in R^3$$ \
    $$ v = (a_1, a_2, a_3) = (0, 1, 0) $$\
    Where, $$ u, v \in w $$\
    For subspace,\
    $$v_{ss1}$$: if $$(a_1, a_2, a_3) = (0, 0, 0) \in R^3$$\
    $$ = 0 + 2 \times 0 - 3 \times 0$$\
    $$= 0 + 0 + 0 $$\
    $$ = 0 \neq 2 $$ \
    $$v_{ss2}$$ :for $$ u, v \in w $$\
    $$ u + w = (1, 2, 1) + (0, 1, 0) $$\
    $$ = (1, 3, 1) $$\
    Now, $$ a_1 + 2a_2 -3a_3 $$\
    $$ =1 + 2\times 3 - 3 \times 1 $$\
    $$ = 1 + 6 -3 $$\
    $$ = 4 \neq 2 $$\
    $$ v_{ss3} $$:for $$ c \in R$\
    $$ cu = c(a_1, a_2, a_3) $$\
    if we choose c = 3 and $$ (a_1, a_2, a_3) = (1, 2, 1) $$\
    $$ cu = 3(1, 2, 1) $$\
    $$ =(3, 6, 3) $$\
    such that, $$ a_1 + 2a_2 - 3a_3 = 3 + 2 \times 6 - 3 \times3 $$\
    $$6$$\
    $$3(2)$$ \
    Hence $$ v_{ss3} $$ holds. Hence the set w is not satisfied all the property of vector subspace hence w is not subspace of $$R^3$$.

