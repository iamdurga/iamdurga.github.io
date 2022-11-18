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

 P(Buy-computer => yes) = Total no of yes/Total class =  9/14 = 0.643 

P(Buy-computer => no) = Total no of no/Total class = 5/14 = 0.357 


`Step II`

 Computation of conditional probability,
 
P(Age => youth/Buy computer => yes) = Total no of youth out of yes/Total yes =  2/9 = 0.222 
 
P(Age => youth/Buy-computer => no) = Total no of youth out of no/Total no =  3/5 = 0.6 
 
P(Income => medium/Buy computer => yes) = Total no of medium out of yes/Total yes =  4/9 = 0.444 

P(income => medium/Buy computer => no) = Total no of medium out of no/Total no =  2/5 = 0.4 

P(student => yes/Buy computer => yes) = Total no  of yes out of yes/Total yes =  6/9 = 0.667 

P(Student => yes/Buy computer => no) = Total no of yes out of no/Total no = 1/5 = 0.2 

P(Credit rating => fair/Buy computer => yes) = Total no of fair out of yes/Total-yes =  6/9 = 0.667 

P(Credit-rating => fair}{Buy computer => no) = Total no of yes out of noTtotal no = 2/5 = 0.4

`Step III` 

Using above probability let's calculate conditional probability

P(features/Buy computer yes) = P(Age => yes/Buy computer => yes) * P(Income => medium}{Buy computer => yes) * P(Student => yes/Buy computer => yes) * P(Credit rating => fair/Buy computer => yes) = 0.222×0.444×0.667×0.667 = 0.044


P(features/Buy computer no) = P(Age => yes/Buy computer => no) * P(Income => medium/Buy computer => no) * P(Student => yes/Buy computer => no) * P(Credit rating => fair/Buy computer => no) = 0.6*0.4*0.2*0.4 = 0.019


`Step IV` 

Computation of Posterior Probability

P(Buy computer => yes/feature) = P(features/Buy computer yes)* P(Buy computer => yes)= 0.044*0.643 = 0.028


P(buy computer => no/feature) = P(features/Buy computer yes)* P(Buy computer => no) = 0.019*0.357 = 0.007



`Conclusion:`
 
Since, 

P(Buy computer => yes/feature) > P(Buy computer => no/feature)

Hence, our final conclusion is classification for given feature is Buy_computer is yes.




```python

```





    



    
