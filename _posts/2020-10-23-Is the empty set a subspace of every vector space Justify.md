---
title:  "Is the empty set a subspace of every vector space? Justify"
date:   2020-10-23 01:29:17 +0545
categories: Linear-Algebra
tags:
  - Vectorspace
  - Basis
header:
  teaser: "assets/header_images/2.png"
  overlay_image: "assets/header_images/7.png"
---
**Question:**a. Is the empty set a subspace of every vector space ? Justify and let  s = $${(a, b, (a + b):a, b \in R)}$$ . Is a subspace of $$R^3$$ under the usual operation.\
b. Let I = (-a , a) a > 0 be an open interval in R let v = Rt the space of all real valued function  define on I. Let $$v_e = {f\in v : f(-x) = f(x)} \forall x \in I $$ the set of all even function on I. And let $$v_o = {f \in v :f(-x) = -f(x)\forall x \in I} $$, the set of all odd function on I. Then show that v = $$ v_e \bigoplus v_0. $$ \

**Solution:**\
The answer is no. The empty set is empty in the sence that it does not contain any elements. Thus a zero vector is not member of the empty set. Without zero we can not say that it is subspace of vector space.\
Here s = $$[a, b, (a + b): a, b \in R] $$\
$$\forall a   \exists –a $$\
$$V_{ss1}: a + (-a) = 0 \in s $$\
$$V_{ss2}: a + b \in s $$\
$$V_{ss3}: for c \in R $$\
s.t $$ ca \in  s$$.\
Hence three condition of vector sub space are satisfy so, s is vector subspace.\

**For solution of b**.\
Here given two function are define by $$v_e = [f \in v : f(-x) = f(x) \forall x \in I]$$  and $$v_0 = [f \in v :f(-x) = -f(x) \forall  x\in I]$$\
First we show that $$v_e$$ and $$v_o$$ are subspace of vector space.\
**For even:**\
Here  $$v_e = [ f \in v : f(-x) = f(x) \forall x \in I]$$\
$$V_{ss1} $$: Since constant function is even . 0 is even function.\
$$0 \in v_e $$\
$$V_{ss2}: \forall x \in I $$\
Let $$ f_1(x), f_2(x) \in v_e $$\
Define, $$f(x) =  f_1(x) + f_2(x)$$\
Now,$$f(-x) =  f_1(-x) + f_2(-x)$$\
=$$f_1(x) + f_2(x)$$\
=$$f(x)$$\
$$V_{ss3}$$: $$\forall c \in R $$\
$$E(x) = c f(x)$$  $$(E(x),f(x) \in v_e, a\in f)$$\
Now, $$E(-x) = cf(-x) = cf(x) = E(x)$$\
Therefore $$E(x) = E(-x)$$\
Hence $$cf(x) \in v_e$$\
Therefore the set of all even function on I i.e; $$v_e$$ is subspace of V.


**For odd:**\
Here $$v_o = [f \in v :f(-x) = -f(x) \forall x\in  I]$$\
$$V_{ss1}$$: Since constant function is odd . 0 is odd function.\
 $$0 \in v_0 $$\
$$V_{ss2}: \forall x \in I$$\
 Let $$f_1(x), f_2(x) \in v_o$$\
 Define, $$f(x) =  f_1(x) + f_2(x)$$\
 Now,$$f(-x) =  f_1(-x) + f_2(-x)$$\
=$$-[f_1(x) + f_2(x)]$$\
=$$-f(x)$$\
$$V_{ss3}: \forall c \in R $$\
$$O(x) = c f(x) (O(x), f(x) \in v_o, a\in f)$$\
Now, $$O(-x) = cf(-x) = -cf(x) = -O(x)$$\
Therefore $$ O(-x) =-O(x)$$\
Hence $$cf(x) \in v_o$$\
From above result we can say that $$v_0$$ is the subspace of V for direct we have to show that
$$ V_e \cap v_o = 0$$\
$$V_e + V_o = V$$\
Also, we need to ahow that these property are unique for this we proceeed as follows,\
Let U be any elenment of $$V_e \cap v_o$$. It means that U is both even and odd function.\
Now, for even function.\
$$U(-x) = U(-x) $$......(1)\
for odd function.\
$$U(-x) = -U(x)$$.......(2)\
From (1) and (2) we can write,\
$$U(x) = -U(x)$$\
$$2U(x) = 0$$\
$$U(x) = 0$$\......(3)
It means that $$V_e \cap v_o = {0}$$. Intersection contains only zero element.\
Also,Let $$f \in N$$\
Clearly,\
$$f(x) = \frac{f(x) + f(-x)}{2} + \frac{f(x) - f(-x)}{2}$$\
$$= g(x) + h(x)$$\
Where,\
$$g(x) = \frac{f(x) + f(-x)}{2}$$\
$$h(x) = \frac{f(x) - f(-x)}{2}$$\
Now,\
$$g(-x) = \frac{f(-x) + f-(-x)}{2}$$\
$$=\frac{f(-x) + f(x)}{2}$$\
$$g(x)$$\
so g(x) is even\
and,$$h(-x) = \frac{f(-x) - f[-(-x)]}{2}$$\
$$= \frac{f(-x) - f(x)}{2}$$\
$$-h(x)$$\
Therefore  $$f = g + h $$. Where g is even and h is odd.\
Uniqueness\
Clearly,\
$$p(x) = \frac{p(x) + p(-x)}{2} + \frac{p(x) - p(-x)}{2}$$\
$$ = m(x) + n(x) $$\
Now,
$$m(-x)= \frac{p(-x) + p(x)}{2}$$\
$$ = \frac{p(x) + p(-x)}{2}$$\
$$ = m(x)$$ .So m(x) is even.\
Similarly,\
$$(-x) =\frac{p(-x)  p(x)}{2}$$\
$$-[\frac{p(x) - p(-x)}{2}]$$\
$$ = - n(x) $$\
Therefore n(-x) = n(x).So n is the odd function.\
p = m + n.Where m is even and n is odd function.\
From above result we see,\
$$v_e \bigoplus v_0.$$.....(4)\
From (3) and (4) we can say that $$ v_e \bigoplus v_0.$$
