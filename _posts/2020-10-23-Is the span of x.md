---
title:  "Is the span of X is X? Does every vector space have finite basis?"
date:   2020-10-23 01:29:17 +0545
categories: Linear-Algebra
tags:
  - Vectorspace
  - Basis
header:
  teaser: "assets/header_images/1.png"
  overlay_image: "assets/header_images/5.png"
---
**Question a:** Is the span of $$ \phi $$ is $$ \phi  $$ ? justify. The vectors $$ u_1 = ( 2, -3 , 1) , u_2 = (1 , 4 , -2) , u_3 = (-8 , 12 , -4) , u_4 = ( 1 , 37 , -17) , u_5 =    (-3 , -5 , 8) $$ generate $$ R^3 $$ . Find a subset of the  set $$ [u_1, u_2, u_3, u_4, u_5] $$.

**Solution:**

First part: \
NO, it is the trivial vector space that includes only the zero vector.

Second part:\
 The vectors $$ u_1 = ( 2, -3 , 1) , u_2 = (1 , 4 , -2), u_3 = (-8 , 12 , -4) , u_4 = ( 1 , 37 , -17) , u_5 = (-3, -5, 8)  $$  generate $$ R^3 $$ . To find the subset we have to search the linearly dependent set from $$ [u_1, u_2, u_3, u_4, u_5] $$.

Let  $$ a_1, a_2, a_3, a_4, a_5 \in R $$.\
Then the linear combination is \
$$ a_1u_1 + a_2u_2 + a_3u_3 + a_4u_4 + a_5u_5 = 0 $$\
 $$ a_1\left[\begin{array}{cc} 2\\-3\\1  \end{array}\right] + a_2 \left[\begin{array}{cc} 1\\4\\-2  \end{array}\right] +a_3\left[\begin{array}{cc} -8\\12\\-4 \end{array}\right] +a_4\left[\begin{array}{cc} 1\\37\\-17  \end{array}\right] + a_5\left[\begin{array}{cc} -3\\5\\8  \end{array}\right] = \left[\begin{array}{cc} 0\\0\\0 \end{array}\right] $$\
 The augmented matrix is,\
 $$ \left[\begin{array}{cc} 2&1&-8&1&-3|0\\-3&4&12&37&5|0\\1&-2&-4&-17&8|0  \end{array}\right] $$

 $$ \left[\begin{array}{cc}
2&\frac{1}{2} & -4 & \frac{1}{2} & \frac{-3}{2}|0\\
-3 & 4 & 12 & 37 & 5|0\\
1 & -2 & -4 & -17 & 8|0  
\end{array}\right] $$ $$ \frac{1}{2}R_1 \Rightarrow R_2 $$

 $$ \left[\begin{array}{cc}
  1 & \frac{1}{2} & -4 & \frac{1}{2} & \frac{-3}{2}|0\\
  0 & \frac{11}{2} & 0 & \frac{77}{2} & \frac{-19}{2}|0\\
  0 & -\frac{-5}{2} & 8 & \frac{-35}{2} & \frac{19}{2}|0
\end{array}\right] $$  $$ R_2 \Leftarrow R_2 +3R_1 $$ , $$ R_3 \Leftarrow R_3 -3 R_1 $$

 $$ \left[\begin{array}{cc}
  1 & \frac{1}{2} & -4 & \frac{1}{2} & \frac{-3}{2}|0\\
  0 & 1 & 0 & 7 & -209|0\\
  0 & -\frac{-5}{2} & 8 & \frac{-35}{2} &\frac{19}{2}|0
\end{array}\right] $$ $$ R_2 \Leftarrow \frac{2}{11}R_2 $$


 $$ \left[\begin{array}{cc}
  1 & \frac{1}{2} & -4 & \frac{1}{2} & \frac{-3}{2}|0\\
  0 & 1 & 0 & 7 & -209|0\\
  0 & 0 & 8 & 0 & -513|0  
  \end{array}\right] $$ $$ R_3 \Leftarrow R_3 +\frac{5}{2} R_2 $$

 $$ \left[\begin{array}{cc}
  1 & 0 & -4 & -3 & 103|0\\
  0 & 1 & 0 & 7 &-209|0\\
  0 & 0 & 8 & 0 & -513|0
\end{array}\right]  $$ $$ R_1 \Leftarrow R_1 -\frac{1}{2}R_2 $$

 $$ \left[\begin{array}{cc}
  1 & 0 & -4 & -3 & 103|0\\
  0 & 1 & 0 & 7 & -209|0\\
  0 & 0 & 1 & 0 & \frac{-513}{8}|0
\end{array}\right] $$ $$ R_3 \Leftarrow \frac{1}{8}R_3 $$

 $$ \left[\begin{array}{cc}
  1 & 0 & 0 & -3 & \frac{-307}{2}|0\\
  0 & 1 & 0 & 7 & -209|0\\
  0 & 0 & 1 & 0 &\frac{-513}{8}|0
\end{array}\right]  $$ R_1 \Leftarrow R_1 + 4R_3 $$

Which shows that the subset of the set $$ [u_1, u_2, u_3, u_4, u_5] $$ that is basis for $$ R^3 $$ are $$ [u_1, u_2, U_3] $$




**Question b:** Does every vector space have finite basis? Justify. Prove that the set of solutions to the system of linear equations 2x – y + z = 0, 3x – 2y + Z = 0 is a subspace of $$ R^3 $$. Find the basis for this $$ R^3 $$.

Solution:\    
First part\
	Every vector space have finite basis is false. The space c[0 , 1] or the space of all 
	Polynomials has no finite basis, only infinite one.

	
  Second part\
			To prove the set of linear equations  $$ 2x – y + z = 0  \\ 3x – 2y + z = 0 $$ is a subspace of $$ R^3 $$.\
			Now\
				Let us denote the solution set by S\
						Where  $$ S = [a(1, 1, -1) : a \in R] $$\
										       $$ = [(a, a, -a): a \in R] $$ is the solutions set 
				of equations  $$ 2x – y + z = 0   3x – 2y + z = 0 $$.\
			Now\
We show S is the subspace of $$ R^3 $$. Clearly S is subspace of $$ R^3 $$.\
 $$ V_{ss1} $$ : Clearly $$ \vec{o} $$  = $$ (0, 0, 0) \in R^3 $$ is a zero vector of $$ R^3 $$ .Now we have to show 0 is zero vector of S. \
             let  $$  \vec{o} = (d, d, -d) \in s $$ \
             such that\
						 $$ u + 0 = u $$   $$ \forall u \in s  $$ \
                        Where  $$ u = (a , a ,-a) $$\
						$$ (a , a , -a) +(d , d , -d) $$ = $$ (a , a , -a) $$  $$ \Rightarrow (d, d,-d) = 0 $$ .\
                        Hence  $$ \vec{o} $$ = $$ (0, 0, 0)  $$ is  solutions to the equcation.\
                        Hence   $$ \vec{o} $$ = $$ (0, 0, 0) \in S $$ \
				$$ V_{ss2} $$ : Let $$ u = (a , a , -a) $$ and $$ v = (b, b, -b) $$ where $$ a, b \in R  $$ and $$ u , v \in S $$\
				Then $$ u + v =  (a , a ,-a) + (b , b , -b) $$
						$$ = (a + b , a + b , -a - b) $$
						$$ =(c , c , -c) $$\
                        where $$ c = a + b $$ and $$ c \in R $$. Hence $$ u + v \in S $$\
			$$ V_{ss3} $$ :Let $$ u = (a , a , -a) $$ and $$ k \in F $$\
				Such that\
                $$ ku = k(a, a , -a) $$\
                $$ = (ka , kb , -kc)\in S $$\. Hence set of solution to the given equations is subspace.
				  $$ 2x – y + z = 0 $$ \
		          $$3x – 2y + Z = 0 $$\
                  By solving we get $$ x = z , z = -y $$. Let $$ x = s , y = s , z = -s $$\
                  we have the solution would be $$ [ ( s , s , - s) = s ( 1 , 1 , -1) : s \in  R ] $$ and basis would be $$ (1, 1, -1) $$.
 
**4.Does the zero vector have no basis? Justify . Construct the real polynomial degree at most 2 whose graph contaions the point $(-4 , 24) ,(1 , 9)  and (3 , 3) $$ sketch the graph.**

Solution:\
      First Part:\
      No,empty set the basis for zero vector.\
	Second part:\
	Here $c_0 = -4, c_1 = 1, c_2 = 3 $$ and $b_0 = 24 , b_1 = 9 , b_2 = 3$\
   Here degree is  at most 2 ,so n = 2\
   Now we find\
	$F_0(x) $$ =$\prod_{(k =0, k \neq 0)}^{2} $$ \
    $F_0(x)$=$\frac{x - ck}{c0 - ck}$\ 
	=$\frac{(x - c_1)(x - c_2)}{(c_0 - c_1)(c_0 - c_1)}$\
	= $\frac{(x-1)(x-3)}{(-4-1)(-4-3)}$\
	=$\frac{x^2 - 4x + 3}{35}$\
	$F_1(x) $$ = $∏_{(k=0, k ≠1)}^{2}\frac{(x-ck)}{(c1-ck)}$\
	= $\frac{(x - c_o)(x - c_2)}{(c_1 - c0)(c_1 - c_2)}$\
	= $\frac{(x + 4)(x - 3)}{(1 + 4)(1 - 3)}$\
	=$\frac{(x_2 + x - 12)}{-10}$\
	$F_2(x) $$ = $\prod_{(k=0, k ≠2)}^{2}\frac{x - ck}{c_2 - c_k}$\
	=$\frac{(x + 4)(x - 1)}{(3 + 4)(3 - 1)}$\
	=$\frac{(x^2 + 3x - 4)}{14}$\
     Hence the require polynomial is\
     $F(x) $$ = $\sum_{(i = 0)}^{2}b_if_i(x)$\
     $= b_0F_0(x) + b_1f_1(x) + b_2f_2(x)$\
	   $F(x) $=$24\frac { (x_2 - 4x + 3)}{35} + 9\frac{(x^2 + x - 12)}{(-10)} +3\frac{(x^2 + 3x - 4)}{14}$\
	                    $$ F(x) = \frac{48(x^2 - 4x + 3)- 63(x^3 + x -12) + 15(x^2 + 3x - 4)}{70}$\
                       $F(x) = \frac{48x^2 - 192x + 144 - 63x^2 -63x + 756 + 15x^2 + 45x - 60}{70}$\
                       $F(x) = \frac{45x - 255x + 900 - 60}{70}$\
                       $F(x) = \frac{(-210 + 840)}{70}$\
	                    $F(x)  = -3x + 12$\
    ![image]({{site.url}}/assets/Math_blog/34.jpg)\
**5.Find row echelon form and reduce row echelon form  A =    $$ \left[\begin{array}{cc} 0&-1 &2&3&4\\2&1&3&4&1\\1&3&-1&2&3\\3&3&-6&4&7 \end{array}\right] $**
        
Solutions:\
Here given matrix is \
A =    $$ \left[\begin{array}{cc} 0&-1 &2&3&4\\2&1&3&4&1\\1&3&-1&2&3\\3&3&-6&4&7 \end{array}\right] $
   
  $\sim \left[\begin{array}{cc} 1&3 &-1&2&3\\2&1&3&4&1\\0&-1&2&3&4\\3&3&-6&4&7 \end{array}\right]  $$ $R_1 \Leftrightarrow R_3$

$\sim  \left[\begin{array}{cc} 1&3 &-1&2&3\\0&-5&5&0&-5\\0&-1&2&3&4\\0&-6&-3&-2&-2 \end{array}\right]  $$  $$ R_2 \Leftarrow R_2 – 2R_1,  R_4 \Leftarrow R_4 – 3R_3$\

 $$ \sim \left[\begin{array}{cc} 1&3 &-1&2&3\\0&1&-1&0&1\\0&-1&2&3&4\\0&-6&-3&-2&-2 \end{array}\right]  $$ $\frac{1}{-5} R_2 \Leftarrow R_2$

$\sim \left[\begin{array}{cc} 1&3 &-1&2&3\\0&1&-1&0&1\\0&0&1&3&5\\0&0&-9&-2&4 \end{array}\right]  $$  $$ R_3 \Leftarrow R_3 + R_2$
$R_4 \Leftarrow R_4 + 6R_2 $

$\sim  \left[\begin{array}{cc} 1&3 &-1&2&3\\0&1&-1&0&1\\0&0&1&3&5\\0&0&0&25&49 \end{array}\right]  $$ $R_4 \Leftarrow R_4 + 9R_3$

$\sim  \left[\begin{array}{cc} 1&3 &-1&2&3\\0&1&-1&0&1\\0&0&1&3&5\\0&0&0&1& \frac{49}{25} \end{array}\right]  $$ $\frac{1}{25}R_4 \Leftarrow R_4 $

Which is row echelon form of a matrix A.\
$\sim  \left[\begin{array}{cc} 1&3 &-1&2&3\\0&1&-1&0&1\\0&0&1&0&\frac{-22}{25}\\0&0&0&1& \frac{49}{25} \end{array}\right] $ $$ R_3 \Leftarrow R_3 - 3 R_4$

$\sim  \left[\begin{array}{cc} 1&3 &-1&2&3\\0&1&0&0&\frac{3}{25}\\0&0&1&0&\frac{-22}{25}\\0&0&0&1& \frac{49}{25} \end{array}\right] $ $$ R_2 \Leftarrow R_2 +  R_3$

$\sim  \left[\begin{array}{cc} 1&3 &-1&0&\frac{-23}{25}\\0&1&0&0&\frac{3}{25}\\0&0&1&0&\frac{-22}{25}\\0&0&0&1& \frac{49}{25} \end{array}\right] $ $$ R_1 \Leftarrow R_1 - 2 R_4$

 $$ \sim \left[\begin{array}{cc} 1&3 &0&0&\frac{-45}{25}\\0&1&0&0&\frac{3}{25}\\0&0&1&0&\frac{-22}{25}\\0&0&0&1& \frac{49}{25} \end{array}\right] $ $$ R_1 \Leftarrow R_1 +  R_3$

$\sim  \left[\begin{array}{cc} 1&0 &0&0&\frac{-54}{25}\\0&1&0&0&\frac{3}{25}\\0&0&1&0&\frac{-22}{25}\\0&0&0&1& \frac{49}{25} \end{array}\right] $ $$ R_1 \Leftarrow R_1 - 3R_3$\
Which is reduced row echelon form of A.