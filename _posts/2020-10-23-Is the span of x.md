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
 
