---
title:  "How Mathematically Naive Bayes Classifier Works?"
date:   2022-10-21 09:29:17 +0545
categories: Machine Learning
tags:
  - Naive Bayes
  - Supervised Learning
  - Classification
header:
  teaser: "assets/monte_carlo/output_8_1.png"
  overlay_image: "assets/monte/output_8_1.png"
toc: true
---

Previously, we wrote blogs on many machine learning algorithms as well as many other topics to help you broaden your knowledge. Please kindly visit our [site](https://dataqoil.com/blog/) and we would be glad if we got some feedback from you to improve our writing. To see some of them, you can follow the mentioned links.
* [Linear Regression](https://dataqoil.com/2022/04/21/fit-linear-regression-using-different-gradient-descent-algorithms/)

* [Logistic Regression](https://dataqoil.com/2020/08/11/writing-a-logistic-regression-class-from-scratch/)

* [K Medoids Clustering ](https://dataqoil.com/2022/02/04/k-medoids-clustering-in-python-from-scratch/)

* [DBSCAN Clustering](https://dataqoil.com/2022/08/05/dbscan-clustering-algorithm/)

* [K Means Clustering](https://dataqoil.com/2022/01/28/kmeans-clustering-in-python-from-scratch/)



Here, in this blog, we are going to discuss the mathematics behind Naivebayes, taking one example problem.

# Introduction to NaiveBayes 

*NaiveBayes is a simple classification algorithm in the machine learning sense. It works on the basis of probability. It calculates the poster's probability using some prior knowledge. It is assumed that each feature used is independent of the other. It is used for multi-class classification problems. When the probability of a particular class is high, then it confirms that features belong in that class. Let's see one example to be clear how Naive Bayes worked Mathematically.*

[Q.N] **Predict class level of the tuple: X = (age = youth, income = medium, student = yes, credit_rating = fair) using Bayesian classification.**


| Age  | income  | Student  | Credit_rating   | Bayes_computer  |
|---|---|---|---|---|
|  youth |high   |  no | fair  | no  |
| youth  | high  |no   | excellent  |no   |
| middle_age  |  high | no  | fair  | yes  |
| senior  |  medium | no  | fair  | yes  |
| senior  |  low | yes  | fair  | yes  |
| senior  |  low | yes  | excellent  | yes  |
| youth  |  medium | no  | fair  | no  |
| youth  |  low | yes  | fair  | yes  |
| senior  |  medium | yes  | fair  | yes  |
| youth  |  medium | yes  | excellent  | yes  |
| middle_age  |  medium | no  | excellent  | yes  |
| middle_age  |  high | yes  | fair  | yes  |
| senior  |  medium | no  | excellent | no  |

**Solution:** 

`Step I`

Prior probability of each class can be computed based on the training tuples
$$ P(Bayes-computer = yes) =\frac{ total-no -of -yes}{total-class} = \frac{ 9}{14} = 0.643 $$

$$ P(Bayes-computer = no) =\frac{ total-no -of -no}{total-class} = \frac{ 5}{14} = 0.357 $$

`Step II`

 Computation of conditional probability,
 
$$P(\frac{Age = youth}{Bayes-computer = yes}) =\frac{ total-no-of-youth-out-of-yes}{total-yes} = \frac{ 2}{9} = 0.222 $$
 
$$P(\frac{Age = youth}{Bayes-computer = no}) =\frac{ total-no-of-youth-out-of-no}{total-no} = \frac{ 3}{5} = 0.6 $$
 
$$P(\frac{income = medium}{Bayes-computer = yes}) =\frac{ total-no-of-medium-out-of-yes}{total-yes} = \frac{ 4}{9} = 0.444 $$

$$P(\frac{income = medium}{Bayes-computer = no}) =\frac{ total-no-of-medium-out-of-no}{total-no} = \frac{ 2}{5} = 0.4 $$

$$P(\frac{student = yes}{Bayes-computer = yes}) =\frac{ total-no-of-yes-out-of-yes}{total-yes} = \frac{ 6}{9} = 0.667 $$

$$P(\frac{student = yes}{Bayes-computer = no}) =\frac{ total-no-of-yes-out-of-no}{total-no} = \frac{ 1}{5} = 0.2 $$

$$P(\frac{credit-rating= fair}{Bayes-computer = yes}) =\frac{ total-no-of-fair-out-of-yes}{total-yes} = \frac{ 6}{9} = 0.667 $$

$$P(\frac{credit-rating = fair}{Bayes-computer = no}) =\frac{ total-no-of-yes-out-of-no}{total-no} = \frac{ 2}{5} = 0.4 $$

`Step III` 

Using above probability let's calculate conditional probability

$$P(\frac{features}{bays-computer-yes})= P(\frac{age= yes}{bayes-computer=yes}) * P(\frac{income= medium}{bayes-computer=yes}) * P(\frac{student= yes}{bayes-computer=yes}) * P(\frac{credit-rating= fair}{bayes-computer=yes})= 0.222×0.444×0.667×0.667 = 0.044
$$

$$P(\frac{features}{bays-computer-no})= P(\frac{age= yes}{bayes-computer=no}) * P(\frac{income= medium}{bayes-computer=no}) * P(\frac{student= yes}{bayes-computer=no}) * P(\frac{credit-rating= fair}{bayes-computer=no})= 0.6*0.4*0.2*0.4 = 0.019
$$

`Step IV` 

Computation of Posterior Probability

$$P(\frac{bayes-computer= yes}{feature}) = P(\frac{features}{bays-computer-yes})* P(bayes-computer = yes)= 0.044*0.643 = 0.028$$


$$P(\frac{bayes-computer= no}{feature}) = P(\frac{features}{bays-computer-yes})* P(bayes-computer = no)= 0.019*0.357 = 0.007
$$


`Conclusion:`
 
Since, 

$$P(\frac{bayes-computer= yes}{feature}) > P(\frac{bayes-computer= no}{feature})$$

Hence, our final conclusion is classification for given feature is bayes_computer is yes.




```python

```





    
