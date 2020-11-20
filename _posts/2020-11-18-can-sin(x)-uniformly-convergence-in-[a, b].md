---
title:  "Can sin(x) Uniformly Convergence On [a, b] 
?"
date:   2020-11-18 01:29:17 +0545
categories: Measure-theory
tags:
  - Pointwise-convergence
  - Uniform-convergence
header:
  teaser: "assets/header_images/7.png"
  overlay_image: "assets/header_images/6.png"
---





8.Show that the function


$$ f(x) = \sin(x) $$
 is uniformly continuous on 
 $$ [0, \infty].$$

Sulution:

For uniformly continious on 
$$ [ 0, \infty] $$ if 
$$ \forall \varepsilon, \exists \delta > 0 , \forall x , y \in  [0, \infty] with | x - y| < \delta 
$$
$$ \Rightarrow | f(x) - f(y) | < \varepsilon 
$$
$$ we have, f(x) = \sin(x) $$
$$ let, we choose \delta = \varepsilon then, x, y \in [0, \infty] with , |x - y | < \delta 
$$

$$ | \sin(x) - \sin(y) |$$

$$\Rightarrow|2\cos\frac{x + y}{2}.\sin\frac{x - y}{2} |
$$

$$\Rightarrow2|\cos\frac{x + y}{2}|.|\sin\frac{x - y}{2}|
$$

$$ Since , |\sin(x) | \leq |x| for all,  X 
$$

$$|\cos(x)| \leq 1 $$

$$ \Rightarrow 2.1.\frac{|x - y|}{2} $$

$$ \Rightarrow |x - y| < \varepsilon $$

Hence, the function $$ f(x) = \sin(x) $$ is uniformly continious on $$ [0, \infty] $$