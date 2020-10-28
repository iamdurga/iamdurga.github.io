---
title:  "Is the zero vector a linear combination of any nonempty set of vectors?"
date:   2020-10-23 01:29:17 +0545
categories: Linear Algebra
tags:
  - Vectorspace
  - Basis
header:
  teaser: "assets/images/what-if.png"
  overlay_image: "assets/images/what-if.png"
---
**Question**: Is the zero vector a linear combination of any nonempty set of vectors ? Justify. Is the set of all differential real valued functions defined on R a subspace of c(R)? Justify your answer.

**Solution**: \
First part:\
Yes,it is \
$$ \vec{0} = 0.\vec{v1} + 0.\vec{v2} + ...+0.\vec{vn} $$\
Moreever, an empty sum, that is the sum of no vectors, is usually define to be zero, and  with that defination 0 is the linear combination of set of vectors, empty or not.\
	Second Part:\
To show differential function is subspace of real valued function define on R a subspace of c(R). Let $$ \mathcal{D}(R) $$ denote the set of all differentiable real valued function over R. If  $$ f : \mathcal {R} \Rightarrow \mathcal{R} $$ is differential then f is continious and so $$ \mathcal{D}(R) $$ is a subset of  $$ \mathcal{C}(R) $$\

We can show that this subset is subspace by showing that this is closed under addition and scalar multiplication, we can proceed as follows.\
If f and g are in  $$ \mathcal{D}(R) $$. Then\
 $$ (f + g)(x) $$ = $$ f(x) + g(x) $$ is define for any  $$ x \in R $$\
			$$ V_{ss1} $$ : Zero is a constant value.\
            We know that differentiation of  constant is zero.\
Thus,  f(x) = 0 \
$$ \forall x\in R $$.
so we have   $$ f \in \mathcal{c}(R) $$ .\
$$ V_{ss2} $$ :Sum of two differential function is also differential.\
We also have differential function is Continuous. \
    Let $$ f(x) \in R\ and\ f(y) \in R $$\
				Then, $$ f(x) + f(y) \in R \Rightarrow f(x) + f(y) \in \mathcal{C}(R)	$$\
	$$ V_{ss3} $$:  Scalar multiplication to any differential function is also differential.
    This implies also Continuous \
             i.e $$ \forall c \in R\ and\ f(x) \in R $$\
						$$ \mathcal{C}f(x) \in (R) \Rightarrow \mathcal{C}f(x) \in \mathcal {C}(R) $$.

