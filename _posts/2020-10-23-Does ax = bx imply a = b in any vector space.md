---
title:  "Does ax = bx imply a = b in any vector space?justify"
date:   2020-10-23 01:29:17 +0545
categories: Linear-Algebra
tags:
  - Vectorspace
  - Basis
header:
  teaser: "assets/head.png"
  overlay_image: "assets/images/what-if.png"
---
**Question:** Does ax = bx imply a = b in any vector space? Justify. Let v = $${(a_1, a_2):a_1, a_2 \in f}$$ where f is field. Define addition of elements of v coordinate wise, and  for $$c \in f$$ and $$(a_1, a_2) \in V$$ . Define $$c(a_1, a_2) = (a_1, 0)$$. Is vector space over F with these operations? Justify your answer by taking all condition of vector space.

Solution:  In any vector space ax = bx implies that a = b false\
It is only true if we take x = 0 \
i.e ; ax = bx \  
x(a – b) = 0 either x = 0 or ( a-b) = 0 \
take x = 0 and any a≠b for x.
						
Let us suppose $$(a_1, a_2), (b_1, b_2) \in V $$ then\
$$V_{s1}: (a_1, a_2) + (b_1, b_2) = (a_1 + b_1, a_2 + b_2) = (b_1 + a_1, b_2 + a_2) = (b_1, b_2) + (a_1, a_2)$$
\
$$V_{s2}: [(a_1, a_2) + (b_1, b_2)] + (c_1, c_2) = (a_1, a_2) + [(b_1 , b_2) + (c_1, c_2)] \forall (c_1, c_2) \in f$$
\
$$V_{s3}: \exists  (d_1, d_2) \in V\ s.t\ (a_1, a_2) + (d_1, d_2) = (a_1, a_2)$$\
$$(a_1, a_2) + (0, 0) = (a_1, a_2)$$\
$$(d_1, d_2) = (0, 0)$$
\
$$V_{s4}: \forall (a_1, a_2) \in V  \exists (-a_1, -a_2) \in V $$\
    s.t $$(a_1, a_2) + (-a_1, -a_2) = (0, 0)$$
\
$$V_{s5}: \forall \in F 1.(a_1, a_2) = (a_1 ,0) = (a_1, 0) ≠ (a_1, a_2)$$\
Hence $$v_{s5}$$ does not satisfy.
\
$$V_{s6}: \forall x, y \in F\  xy(a_1, a_2)  = x(ya_1, 0)$$
\
$$V_{s7}: \forall x, y \in F $$\
$$(x + y)(a_1, a_2) $$   
= $$[(x + y)a_1, 0]$$\
= $$ [xa_1 + ya_1, 0]$$\
= $$ (xa_1, 0) + (ya_1, 0)$$
\
$$V_{s8}: \forall x \in f $$
\
$$x[(a_1, a_2) + (b_1, b_2)]$$
		=$$x[a_1 + b_1, a_2 + b_2]$$\
		=$$[x(a_1 + b_1), 0]$$\
		=$$(xa_1, 0) + (xb_1, 0)$$\
		=$$ x(a_1, a_2) + x(b_1, b_2)$$\

$$ V_{s5} $$ does not satisfy it is not vector space.

**Question:** Does ax = bx imply x = y in any vector space? Justify. Let v denote the set of ordered pairs of real numbers.if $$(a_1, a_2)$$ and $$(b_1, b_2)$$ are element of v and $$c \in R$$ , define $$(a_1 , a_2) + (b_1 , b_2) = (a_1.b_1, a_2 + b_2)$$ and $$c(a_1, a_2) = (a_1, ca_2)$$. Is v a vector space over R with these operations ? Justify your answer by showing all conditions of vector space.

**Solution**:
 In any vector space ax = ay implies that  x = y is false.\
 It is only true if we take a = 0\
		i.e;  ax = ay     a(x – y)  = $$0 \in V$$ \
		either a = 0  , or ( x – y) = 0    if we take a = 0 and any x ≠ y for a.\

**Second part**\
Here  v denote the set of ordered pairs of real numbers. If $$(a_1, a_2) and\ (b_1, b_2)$$ are element of v and $$c \in R $$,define $$(a_1 , a_2) + (b_1 , b_2) = (a_1.b_1, a_2 + b_2)$$ and $$c(a_1, a_2) = (a_1, c.a_2)$$.\
$$V_{s1}: (a_1, a_2) + (b_1 , b_2) = (a_1.b_1, a_2 + b_2)  =  (b_1.a_1 , b_2 + a_2) = (b_1, b_2) + (a_1, a_2)$$\
$$V_{s2}: \in  [(a_1, a_2)  + (b_1, b_2)] + (c_1, c_2)  = (a_1.b_1, a_2 + b_2) + (c_1, c_2)$$\  
=  $$(a_1.b_1.c_1 , a_2 + b_2 + c_2)  =  (a_1, a_2) + (b_1.c_1 , b_2 + c_2) = (a_1, a_2) + [(b_1, b_2) + (c_1 , c_2)]$$\
$$V_{s3}: \exists (d_1, d_2) \in V $$\
s.t $$ (a_1, a_2) + (d_1, d_2) = (a_1, a_2)$$\
Or,$$ (a_1.b_1 , a_2 + b_2 ) = (a_1 , a_2) \Rightarrow  a_1.b_1 = a_1  \Rightarrow b_1 = 1$$\
Also,$$ a_2 + b_2 = a_2  \Rightarrow  b_2 = 0$$\
Hence $$ (d_1, d_2) = (1, 0)$$\
so, $$(a_1, a_2) + (d_1, d_2) ≠ (a_1 , a_2)$$\
$$v_{s3}$$ does not satisfy.\
$$V_{s4}: \forall (a_1 , a_2) \exists (-a_1, -a_2) \in V $$
s.t  $$(a_1, a_2) + (-a_1 , -a_2) = [a_1.(-a_1) , b_1 + (-b_1) ] = (-a_1^2, 0)≠0 $$\
Hence $$v_{s4}$$ also not satisfy.\
$$V_{s5}: for 1\in R 1.(a_1, a_2)  = (a_1, 1.a_2) = (a_1, a_2)$$\
$$V_{s6}: \forall x, y \in R $$\
$$xy(a_1, a_2) = x(a_1, ya_2) = x[y(a_1, a_2)$$\
$$V_{s7}: \forall x, y \in R$$ \
$$(x + y) [(a_1, a_2) + (b_1 , b_2)] = (x + y)(a_1, a_2) + (x + y) (b_1, b_2)$$\
L.H.S	= $$(x + y)(a_1.b_1, a_2 + b_2)$$\
    = $$[a_1.b_1  , (x + y)(a_2 + b_2)] $$\
    =$$[a_1.b_1 , (x + y) a_2 + (x + y) b_2]$$\
	R.H.S  = $$[ a_1 , (x + y)a_2] + [b_1 , (x + y)b_2]$$\
    = $$[a_1.b_1 , (x + y)a_2 + (x + y) b_2]$$\
    L.H.S = R.H.S\
$$V_{s8}:  \forall  x \in R $$\
$$x[(a_1, a_2) + (b_1, b_2)]  = x(a_1, a_2) + y(b_1, b_2)$$
	L.H.S\
    = $$x[ a_1.b_1 , a_2 + b_2]$$\
    = $$[a_1.b_1 , x(a_2 + b_2)]$$\
    = $$[a_1.b_1 , xa_2 + xb_2]$$\
	R.H.S\
    = $$(a_1 , xa_2) + (b_1 , xb_2) = (a_1.b_1 , xa_2 + xb_2)$$\
    L.H.S = R.H.S \
    Here $$v_{s3}$$ and $$ v_{s4} $$ are not satisfy. Hence it is not vector space.

