---
title:  "Is If x Belong To The Domain Than f(x) belong To The Range
?"
date:   2020-11-18 01:29:17 +0545
categories: Measure-theory
tags:
  - Converse
  - Inverse
header:
  teaser: "assets/header_images/2.png"
  overlay_image: "assets/header_images/3.png"
---

Let 
 $$ F : x \Rightarrow y $$

be a function. Then prove that

$$
i.  A_1 \subset A_2   \Rightarrow  F(A_1)  \subset  F(A_2) \\  
ii. F(\cup_i A_i)  = \cup_i F(A_i) \\ 
iii.F(\cap_i A_i) \subset \cap_i f(A_i) 
$$

Solution:

$$ Let \ f: x \rightarrow y $$ be a funxtion.

i.

$$Let\ y \in f(A_1)$$ 
$$Then\ \exists x \in A_1 : y = f(x) $$.
$$ But\ A_1 \subset A_2 $$
$$ we\ can\ say\ , x \in A_2 $$ 
$$ Hence\ y = f(x) $$

ii.

$$ 
Let\  y \in f ( \cup_i A_i) then\ \exists x \in \cup_i A_i : y = f(x)
$$

$$ Since\  x \in (\cup_iA_i) \Rightarrow  x \in A_i\ for\ some\ i $$

$$ so\  y = f(x) \in f(A_i)\  and\ hence\  y \in \cup_i(A_i) $$

Conversely

$$ Let\  y \in \cup_if(A_i)\ then\ y \in f(A_i) for\ some\ i $$

$$ so\  \exists x \in A_i : y = f(x) $$

$$ and\ x \in \Rightarrow x \in \cup_i(A_i) $$

$$ so\ that\  f(x) \in f(\cup_i A_i)$$

iii.

$$ 
Let\ y \in f(\cup_i A_i)\ then\ \exists x \in \cap_i A_i : y = f(x) 
$$

$$ Since\ x \in \cap_i A_i $$

$$ we\ can\ write\  x \in A_i\ for\  all\ i $$

$$ so\  f(x)  \in f(A_i)\ for\ all\  i $$

$$ Hence\ f(x) \in \cap_if(A_i) $$