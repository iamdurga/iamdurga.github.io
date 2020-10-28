---
title:  "Example of row echelon form and reduce row echelon form of matrix."
date:   2020-10-23 01:29:17 +0545
categories: Linear Algebra
tags:
  - Vectorspace
  - Basis
header:
  teaser: "assets/images/what-if.png"
  overlay_image: "assets/images/what-if.png"
---
**Question:** Find row echelon form and reduce row echelon form  A =    $$ \left[\begin{array}{cc} 0&-1 &2&3&4\\2&1&3&4&1\\1&3&-1&2&3\\3&3&-6&4&7 \end{array}\right] $$ 
<br/>   
Solution:

Here given matrix is \
A =    $$ \left[\begin{array}{cc} 0&-1 &2&3&4\\2&1&3&4&1\\1&3&-1&2&3\\3&3&-6&4&7 \end{array}\right] $$ 
   
$$ \sim \left[\begin{array}{cc} 1&3 &-1&2&3\\2&1&3&4&1\\0&-1&2&3&4\\3&3&-6&4&7 \end{array}\right] \ R_1 \Leftrightarrow R_3$$

$$ \sim  \left[\begin{array}{cc} 1&3 &-1&2&3\\0&-5&5&0&-5\\0&-1&2&3&4\\0&-6&-3&-2&-2 \end{array}\right]  \ R_2 \Leftarrow R_2 – 2R_1,  R_4 \Leftarrow R_4 – 3R_3 $$

 $$ \sim \left[\begin{array}{cc} 1&3 &-1&2&3\\0&1&-1&0&1\\0&-1&2&3&4\\0&-6&-3&-2&-2 \end{array}\right]  \ \frac{1}{-5} R_2 \Leftarrow R_2 $$

$$ \sim \left[\begin{array}{cc} 1&3 &-1&2&3\\0&1&-1&0&1\\0&0&1&3&5\\0&0&-9&-2&4 \end{array}\right]  \ R_3 \Leftarrow R_3 + R_2 \ R_4 \Leftarrow R_4 + 6R_2 $$ 

$$ \sim  \left[\begin{array}{cc} 1&3 &-1&2&3\\0&1&-1&0&1\\0&0&1&3&5\\0&0&0&25&49 \end{array}\right]  \ R_4 \Leftarrow R_4 + 9R_3 $$

$$\sim  \left[\begin{array}{cc} 1&3 &-1&2&3\\0&1&-1&0&1\\0&0&1&3&5\\0&0&0&1& \frac{49}{25} \end{array}\right]  \ \frac{1}{25}R_4 \Leftarrow R_4 $$ 

Which is row echelon form of a matrix A.
Now reduced echelon form,

$$\sim  \left[\begin{array}{cc} 1&3 &-1&2&3\\0&1&-1&0&1\\0&0&1&0&\frac{-22}{25}\\0&0&0&1& \frac{49}{25} \end{array}\right] \ R_3 \Leftarrow R_3 - 3 R_4$$

$$\sim  \left[\begin{array}{cc} 1&3 &-1&2&3\\0&1&0&0&\frac{3}{25}\\0&0&1&0&\frac{-22}{25}\\0&0&0&1& \frac{49}{25} \end{array}\right] \ R_2 \Leftarrow R_2 +  R_3$$

$$\sim  \left[\begin{array}{cc} 1&3 &-1&0&\frac{-23}{25}\\0&1&0&0&\frac{3}{25}\\0&0&1&0&\frac{-22}{25}\\0&0&0&1& \frac{49}{25} \end{array}\right] \ R_1 \Leftarrow R_1 - 2 R_4$$

 $$ \sim \left[\begin{array}{cc} 1&3 &0&0&\frac{-45}{25}\\0&1&0&0&\frac{3}{25}\\0&0&1&0&\frac{-22}{25}\\0&0&0&1& \frac{49}{25} \end{array}\right] \ R_1 \Leftarrow R_1 +  R_3$$

$$\sim  \left[\begin{array}{cc} 1&0 &0&0&\frac{-54}{25}\\0&1&0&0&\frac{3}{25}\\0&0&1&0&\frac{-22}{25}\\0&0&0&1& \frac{49}{25} \end{array}\right] \ R_1 \Leftarrow R_1 - 3R_3 $$\
Which is reduced row echelon form of A.