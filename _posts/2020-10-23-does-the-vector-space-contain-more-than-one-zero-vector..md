---
title: "Does the vector space contain more than one zero vector?"
date:   2020-10-23 01:29:17 +0545
categories: Linear Algebra
tags:
  - Vectorspace
  - Basis
header:
  teaser: "assets/images/head.png"
  overlay_image: "assets/images/what-if.png"
---
# Homework Assigment 1 of linear Algebra
 Solution set  1

Excercise.
**1.Does every vector space contain a zero vector? Justify.Let s = {0,1} and f = R in f(S, R) . Show that f = g and f + g = h where f(t) = 2t + 1 , $ g(t) = 1 + 4t - 2t^2$ and h(t) = 5t + 1.**


Solution:Yes, every vector space contaion a Zero vector . Zero vector is a identity  under addition. To be vector space it is necessary to satisfy identity property.

  **Second part**
  
 Here s = { 0, 1} and f  = R in F (S, R)
 
 also,\
 f(t) = 2t + 1, g(t) = 1 + 4t – 2$t^2$ and h(t) = 5t + 1 .
 
 Take t = 0 
 
 f(0) = 2.0 + 1 = 1
 
		g(0) = 1 + 4.0 – 2.(0)^2 = 1
        
		h(0) = 50 + 1 = 2 
        
        hence f(0) = g(0) so f(t) = g(t)
        
Take  t = 1 

f(1) = 2.1 + 1 = 3

		g(1) = 1 + 4.1 – 2.(1)^2 = 3
        
		h(1) = 51 + 1 = 6  
        
        hence f(1) + g(1)  = h(1)
        
        so f(t) + g(t) = h(t)  verified.
        
        
**2.May a vector space have more than one zero vector?justify. Let $v = {(a_1, a_2):a_1, a_2 \in R}$. for $(a_1, a_2)$, $(b_1, b_2)$ = $(a_1 + 2b_1,  a_2 + 3b_2)$ and $c(a_1, a_2)$ = $(ca_1, a_2)$.Is v a vector space over f with these operations?justify your answer.**

Solution:\
Let a vector space have two zeros say 0 and 0^' . From $v_{s3}$  0 is the identity  under addition\
 Hence $ \forall  x \in V$\
             x + 0 = 0 + x = x............(1)\
             also from $v_{s3}$   0' is identity under addition.\
             x + 0' = 0' + x = x..........(2)\
            From (1) and (2)\
            x + 0 = x +$0^'$  = x .\
            Hence there is unique zeros in vector space.
            
**Second part**

Here given\
v = ${(a_1, a_2):a_1, a_2 \in R}$ for $(a_1, a_2)$, $(b_1, b_2) \in V$ and $c \in R$ \
Define $(a_1, a_2) + (b_1 , b_2)$ = $(a_1 + 2b_1,  a_2 + 3b_2)$ and $c(a_1, a_2)$  =  $(ca_1, a_2)$\
$V_{s1}:$ for $(a_1, a_2)$, $(b_1, b_2) \in V$   $(a_1, a_2) + (b_1, b_2)$  =  $(a_1 + 2a_2, b_1 + 3b_2)$ $\neq$ $(a_2 + 2a_1, b_2 + 3b_1)$ $\neq$ $(b_1, b_2) + (a_1, a_2)$\
$V_{s1}$ does not hold.\
$V_{s2}$: for $(a_1, a_2)$, $(b_1, b_2) \in V$ and $ (c_1, c_2) \in V $\
          $[(a_1, a_2) + (b_1, b_2)] + (c_1, c_2)$  = $[ a_1 + 2b_1, a_2 + 3b_2] + (c_1, c_2)$ $ \neq$ $ (a_1 + 2b_1 + c_1,  a_2 + 3b_2 + 3b_3) $ $\neq$ $(a_1, a_2)$ + $[ b_1 + 2c_1, b_2 + 3c_2]$ $ \neq $ $(a_1, b_2)$ + $[(b_1, b_2) + (c_1, c_2)]$\
          $V_{s2}$ does not hold.\
$V_{s3}$:if there exsist a element  z = $(d_1, d_2) \in V$ such that $(a_1, a_2) + (d_1, d_2)$ = $(a_1, a_2)$\
	$(a_1 + 2d_1, a_2 + 3d_2) $ = $(a_1, a_2)$\
                   	 $ a_1 + 2d_1$  = $a_1$ $\Rightarrow d_1 = 0$\
 	$a_2 + 3d_2$  = $a_2 \Rightarrow d_2 = 0$\
    This show that $(a_1, a_2) + (0, 0)$ = $(a_1, a_2)$\
$v_{s4}$:Let $ \forall$  $(a_1, b_1)$$ \exists (-a_1, -a_2) \in V$\  
such that$ (a_1, a_2) + (-a_1, -a_2)$ = $[a_1 +(-2a_1), a_2 + (-3a_2)]$ = $(-a_1, -2a_2)$ $\neq (0, 0)$ .\
Hence$ v_{s4}$ does not satisfy.\
$V_{s5}$: $1 \in  F$ $ 1.(a_1, b_1)$ = $(1.a_1, b_1)$ =$ (a_1, b_1)$\
$V_{s6}$: $\forall x, y \in F $$xy(a_1, b_1)$ = $ x(ya_1, b)$ = $x[y(a_1, b1)]$\
$V_{s7}$:$ \forall x, y \in F$ (x+y) $(a_1, b_1)$  = $[(x+y)a_1, b_1]$ = $(xa_1  + ya_1, b_1)$\
                       also $x(a_1, b_1)$ + $y(a_1, b_2)$ = $(xa_1, b_1)$ + $(ya_1, b_1)$  = $(xa_1 + ya_1, b_1 + b_2)$ = $(xa_1 + ya_1, 2b_1)$\
                    (x+y)$(a_1, b_1) $ ≠ $x(a_1, b_1) + y(a_1, b_1)$\
                    Hence $v_{s7}$ does not satisfy.\
$V_{s8}$: $ \forall  x \in F$  $  x[(a_1, b_1) + (a_2, b_2)]$  = $x(a_1, b_1) + x(a_2, b_2) $ = $(xa_1, b_1) + (xa_2, b_2)$\
All the condition of vector space does not satisfy hence it is not vector space.

**3.Does ax = bx imply a = b in any vector space? Justify.let v = ${(a_1, a_2):a_1, a_2 \in f}$ where f is field. Define addition of elements of v coordinate wise, and  for $ c \in f$ and $(a_1, a_2) \in V$ . Define $c(a_1, a_2)$ = $(a_1, 0)$ .Is vector space over F with these operations? Justify your answer by taking all condition of vector space.**

Solution:  In any vector space ax = bx implies that a = b false\
It is only true if we take x = 0 \
i.e ; ax = bx \  
x(a – b) = 0 either x = 0 or ( a-b) = 0 \
take x = 0 and any a≠b for x.
						
Let us suppose $(a_1, a_2)$, $(b_1, b_2) \in V $ then\
$V_{s1}$: $(a_1, a_2)$ + $(b_1, b_2)$ =$ (a_1 + b_1, a_2 + b_2)$ = $(b_1 + a_1, b_2 + a_2)$ = $(b_1, b_2) + (a_1, a_2)$\
$V_{s2}$: $ [(a_1, a_2) + (b_1, b_2)] + (c_1, c_2) $ = $ (a_1, a_2) + [(b_1 , b_2) + (c_1, c_2)]$ $ \forall (c_1, c_2) \in f$\
$V_{s3}$: $ \exists  (d_1, d_2) \in V $ s.t $(a_1, a_2) + (d_1, d_2) $ = $(a_1, a_2)$ \
 			$ (a_1, a_2) + (0, 0) $ =$ (a_1, a_2) $ \
	$ (d_1, d_2)$ = $(0, 0)$\
$V_{s4}$:$ \forall (a_1, a_2) \in V  \exists (-a_1, -a_2) \in V $\
    s.t $ (a_1, a_2) + (-a_1, -a_2)$ = $(0, 0)$
$V_{s5}$: $\forall \in F 1.(a_1, a_2) $ = $(a_1 ,0)$ = $(a_1, 0)$ ≠ $(a_1, a_2)$\
Hence $ v_{s5}$ does not satisfy.
$V_{s6}$:$ \forall x, y \in F $ $ xy(a_1, a_2)$  = $x(ya_1, 0)$ 
$V_{s7}$: $\forall x, y \in F $\
$(x + y)(a_1, a_2) $    
		= $[(x + y)a_1, 0]$
		=$ [xa_1 + ya_1, 0]$
		=$(xa_1, 0) + (ya_1, 0)$
		
$V_{s8}$: $\forall x \in f $\
$x[(a_1, a_2) + (b_1, b_2)]$
		= $x[a_1 + b_1, a_2 + b_2]$
		=$[x(a_1 + b_1), 0]$
		=$(xa_1, 0) + (xb_1, 0)$
		=$ x(a_1, a_2) + x(b_1, b_2)$\
$V_{s5}$ does not satisfy it is not vector space.\
**4.Does ax = bx imply x = y in any vector space? justify. let v denote the set of ordered pairs of real numbers.if $(a_1, a_2)$ and $(b_1, b_2)$ are element of v and $c \in R$ , define $(a_1 , a_2)$ + $(b_1 , b_2)$ =$ (a_1.b_1, a_2 + b_2)$ and $ c(a_1, a_2)$ = $(a_1, ca_2)$ . Is v a vector space over R with these operations ? Justify your answer by showing all conditions of vector space**\
Solution\
 In any vector space ax = ay implies that  x = y is false.\
 It is only true if we take a = 0\
		i.e;  ax = ay     a(x – y)  = $0 \in V$ \
		either a = 0  , or ( x – y) = 0    if we take a = 0 and any x ≠ y for a.\
**Second part**\
Here  v denote the set of ordered pairs of real numbers. If $(a_1, a_2) $and $(b_1, b_2)$ are element of v and $c \in R $ ,define $(a_1 , a_2)$ + $(b_1 , b_2)$ = $(a_1.b_1, a_2 + b_2)$ and $ c(a_1, a_2)$ = $(a_1, c.a_2)$.\
$V_{s1}$:$ (a_1, a_2) + (b_1 , b_2)$   = $(a_1.b_1, a_2 + b_2)$  =  $(b_1.a_1 , b_2 + a_2)$  =$ (b_1, b_2) + (a_1, a_2)$\
$V_{s2}$: $ \in  [(a_1, a_2)  + (b_1, b_2)] + (c_1, c_2)$  = $ (a_1.b_1, a_2 + b_2) + (c_1, c_2)$  =  $(a_1.b_1.c_1 , a_2 + b_2 + c_2)$  =  $(a_1, a_2) + (b_1.c_1 , b_2 + c_2)$ = $(a_1, a_2) + [(b_1, b_2) + (c_1 , c_2)]$\
$V_{s3}$:  $\exists$$ (d_1, d_2) \in V $\
s.t$ (a_1, a_2) + (d_1, d_2)$ = $(a_1, a_2)$\
Or,$ (a_1.b_1 , a_2 + b_2 )$ =$ (a_1 , a_2) \Rightarrow  a_1.b_1 = a_1  \Rightarrow b_1 = 1$\
Also,$ a_2 + b_2$ = $a_2  \Rightarrow  b_2 = 0$\
Hence$ (d_1, d_2)$ = $(1, 0)$\
so, $(a_1, a_2) + (d_1, d_2)$ ≠ $(a_1 , a_2)$\
$v_{s3}$ does not satisfy.\
$V_{s4}$: $ \forall (a_1 , a_2) \exists (-a_1, -a_2) \in V $
s.t  $(a_1, a_2) + (-a_1 , -a_2)$ = $[a_1.(-a_1) , b_1 + (-b_1) ]$ =$ (-a_1^2, 0)≠0$\
Hence $v_{s4}$ also not satisfy.\
$V_{s5}$: for $1\in R$ $ 1.(a_1, a_2)  = (a_1, 1.a_2) = (a_1, a_2)$\
$V_{s6}$: $ \forall x, y \in R $\
$xy(a_1, a_2)$ =$ x(a_1, ya_2)$ = $x[y(a_1, a_2)$\
$V_{s7}$:$ \forall x, y \in R$ \
$(x + y) [(a_1, a_2) + (b_1 , b_2)] $=$ (x + y)(a_1, a_2) + (x + y) (b_1, b_2)$\
	L.H.S	= $(x + y)(a_1.b_1, a_2 + b_2)$\
    = $ [a_1.b_1  , (x + y)(a_2 + b_2)] $\
    =$[a_1.b_1 , (x + y) a_2 + (x + y) b_2]$\
	R.H.S  = $[ a_1 , (x + y)a_2] + [b_1 , (x + y)b_2]$\
    = $[a_1.b_1 , (x + y)a_2 + (x + y) b_2]$\
    L.H.S = R.H.S\
$V_{s8}$:  $\forall  x \in R $\
$x[(a_1, a_2) + (b_1, b_2)]$  =$ x(a_1, a_2) + y(b_1, b_2)$
	L.H.S\
    = $ x[ a_1.b_1 , a_2 + b_2]$\
    = $ [a_1.b_1 , x(a_2 + b_2)]$\
    = $[a_1.b_1 , xa_2 + xb_2]$\
	R.H.S\
    = $(a_1 , xa_2) + (b_1 , xb_2)$ = $(a_1.b_1 , xa_2 + xb_2)$\
    L.H.S = R.H.S \
    Here$ v_{s3}$ and$ v_{s4} $ are not satisfy .Hence it is not vector space.

**5.\
a. Is the empty set a subspace of every vector space ? Justify and let  s = ${(a, b, (a + b):a, b \in R)}$ . Is a subspace of $R^3$ under the usual operation.\
b. Let I = (-a , a) a > 0 be an open interval in R let v = Rt the space of all real valued function  define on I. Let $ v_e$ = ${f\in v : f(-x) = f(x)}$ $ \forall x \in I $ the set of all even function on I. And let $v_o$ =$ {f \in v :f(-x) = -f(x)\forall x \in I} $ ,the set of all odd function on I.Then show that v = $ v_e \bigoplus v_0.$** \
**Solution:**\
The answer is no.The empty set is empty in the sence that it does not contain any elements.Thus a zero vector is not member of the empty set. Without zero we can not say that it is subspace of vector space.\
 Here s = $[a, b, (a + b): a, b \in R] $ \
 $\forall a   \exists –a $\
 $V_{ss1}: a + (-a) = 0 \in s $\
$V_{ss2}: a + b \in s$\
$V_{ss3}: for c \in R $\
s.t$ ca \in  s$ .\
Hence three condition of vector sub space are satisfy so, s is vector subspace.\
**For solution of b**.\
Here given two function are define by $v_e$ = $[f \in v : f(-x) = f(x) \forall x \in I]$  and $v_0 $=$ [f \in v :f(-x) = -f(x) \forall  x\in I]$\
First we show that $v_e$ and $v_o$ are subspace of vector space.\
**For even:**\
Here  $v_e$ = $[ f \in v : f(-x) = f(x) \forall x \in I]$\
$V_{ss1}$: Since constant function is even . 0 is even function.\
 $ 0 \in v_e $\
$V_{ss2}$: $ \forall x \in I$\
 Let $f_1(x)$, $f_2(x) \in v_e$\
 Define, $f(x) =  f_1(x) + f_2(x)$\
 Now,$f(-x) =  f_1(-x) + f_2(-x)$\
=$f_1(x) + f_2(x)$\
=$f(x)$\
$V_{ss3}$: $\forall c \in R $\
$E(x) = c f(x)$  $ (E(x),f(x) \in v_e, a\in f)$\
Now, $ E(-x) = cf(-x) = cf(x) = E(x)$\
Therefore $E(x) = E(-x)$\
Hence $cf(x) \in v_e$\
Therefore the set of all even function on I i.e; $v_e$ is subspace of V.\


**For odd:**\
Here $v_o = [f \in v :f(-x) = -f(x) \forall x\in  I]$\
$V_{ss1}$: Since constant function is odd . 0 is odd function.\
 $ 0 \in v_0 $\
$V_{ss2}$: $ \forall x \in I$\
 Let $f_1(x)$, $f_2(x) \in v_o$\
 Define, $f(x) =  f_1(x) + f_2(x)$\
 Now,$f(-x) =  f_1(-x) + f_2(-x)$\
=$-[f_1(x) + f_2(x)]$\
=$-f(x)$\
$V_{ss3}$: $\forall c \in R $\
$O(x) = c f(x)$  $ (O(x),f(x) \in v_o, a\in f)$\
Now, $ O(-x) = cf(-x) = -cf(x) = -O(x)$\
Therefore $O(-x) =-O(x)$\
Hence $cf(x) \in v_o$\
From above result we can say that $v_0$ is the subspace of V for direct we have to show that
$ V_e \cap v_o = 0$\
$V_e + V_o = V$\
Also, we need to ahow that these property are unique for this we proceeed as follows,\
Let U be any elenment of $ V_e \cap v_o$ .It means that U is both even and odd function.\
Now, for even function.\
$U(-x) = U(-x) $......(1)\
for odd function.\
$U(-x) = -U(x)$.......(2)\
From (1) and (2) we can write,\
$U(x) = -U(x)$\
$2U(x) = 0$\
$U(x) = 0$\......(3)
It means that $ V_e \cap v_o = {0}$.Intersection contains only zero element.\
Also,Let $ f \in N$\
Clearly,\
$f(x) = \frac{f(x) + f(-x)}{2} + \frac{f(x) - f(-x)}{2}$\
$= g(x) + h(x)$\
Where,\
$g(x) = \frac{f(x) + f(-x)}{2}$\
$h(x) = \frac{f(x) - f(-x)}{2}$\
Now,\
$g(-x) = \frac{f(-x) + f-(-x)}{2}$\
$=\frac{f(-x) + f(x)}{2}$\
$g(x)$\
so g(x) is even\
and,$h(-x) = \frac{f(-x) - f[-(-x)]}{2}$\
$= \frac{f(-x) - f(x)}{2}$\
$-h(x)$\
Therefore  $ f = g + h $ . Where g is even and h is odd.\
Uniqueness\
Clearly,\
$p(x) = \frac{p(x) + p(-x)}{2} + \frac{p(x) - p(-x)}{2}$\
$ = m(x) + n(x) $\
Now,
$m(-x)= \frac{p(-x) + p(x)}{2}$\
$ = \frac{p(x) + p(-x)}{2}$\
$ = m(x)$ .So m(x) is even.\
Similarly,\
$(-x) =\frac{p(-x)  p(x)}{2}$\
$-[\frac{p(x) - p(-x)}{2}]$\
$ = - n(x) $\
Therefore n(-x) = n(x).So n is the odd function.\
p = m + n.Where m is even and n is odd function.\
From above result we see,\
$v_e \bigoplus v_0.$.....(4)\
From (3) and (4) we can say that$ v_e \bigoplus v_0.$
