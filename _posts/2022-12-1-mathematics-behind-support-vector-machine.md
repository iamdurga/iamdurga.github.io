---
title:  "Mathematics Behind Support Vector Machine"
date:   2022-12-1 07:29:17 +0545
categories: Data Science
tags:
  - Outliers
  - Data Science
  - Classification
header:
  teaser: "assets/outlier/outlier.png"
  overlay_image: "assets/outlier/outlier.png"
toc: true
---
Previously, we wrote blogs on many machine learning algorithms (Classification, Predication) as well as many other topics to help you sharpen your knowledge of how machine work. Please kindly visit our [site](https://dataqoil.com/blog/) and we would be happy if we got some feedback from you to improve our writing. To see some of them, you can follow the mentioned links.

* [Linear Regression](https://dataqoil.com/2022/04/21/fit-linear-regression-using-different-gradient-descent-algorithms/)

* [Logistic Regression](https://dataqoil.com/2020/08/11/writing-a-logistic-regression-class-from-scratch/)

* [K Medoids Clustering ](https://dataqoil.com/2022/02/04/k-medoids-clustering-in-python-from-scratch/)

* [DBSCAN Clustering](https://dataqoil.com/2022/08/05/dbscan-clustering-algorithm/)

* [K Means Clustering](https://dataqoil.com/2022/01/28/kmeans-clustering-in-python-from-scratch/)

In this blog, we are going to discuss how mathematical support vector machine works. We will also discuss the types of SVM and how to implement it in Python. So, let's get started.

## Introduction
One of the most widely used supervised learning techniques, Support Vector Machine (SVM), is utilized for both classification and regression issues. However, it is largely employed in Machine Learning Classification issues.

When given input data points, a support vector machine generates the hyperplane which in two dimensions is just a line that best divides the data points into two groups.

The decision boundary is this line or hyperplane; any data points that fall on one side of it are categorized in one class, and those that fall on the other side are classified in a different class.

![image]({{site.url}}/assets/SVM/figure1.png)

They offer two key advantages over more recent algorithms like neural networks: greater speed and improved performance with fewer samples (in the thousands). The nearest data points to the hyperplane, known as support vectors, have an impact on the hyperplane's position and orientation. There are a variety of different hyperplanes that might be used to split the two classes of data points.

SVM algorithm chooses the hyperplane with the highest margin as the ideal hyperplane. Maximum marginal hyperplane is the name of such a hyperplane (MMH). Let H1 and H2 be parallel to the decision boundary's hyperplane and pass through the support vectors.

It should be the same distance between plane H1 and the hyperplane as between plane H2 and the hyperplane. The margin is the separation of planes H1 and H2.

![image]({{site.url}}/assets/SVM/figure2.png)

## Types of Support Machine

There are two varieties of Support Vector Machine (SVM): Linear SVM and Non-linear SVM.

The SVM used to categorize data points with linear separability is known as linear SVM, whereas the SVM used to categorize data points with non-linear separability is known as non-linear SVM.

![image]({{site.url}}/assets/SVM/figure3.png)

Non-linear SVM operates in the subsequent two steps:

* By employing the kernel-trick, it converts low-dimensional data points into high-dimensional data points that can be linearly separated.

* Then, it uses linear-hyperplane to classify the data points.

The kernel of SVM algorithms is a collection of mathematical functions. Non-linearly separable low-dimensional data points are converted into linearly separable high-dimensional data points using these functions. Popular kernels include the Gaussian, Linear, Polynomial, Radial Basis Function (RBF), Sigmoid, and others.

Consider the following linearly inseparable 2-D data items. By including the third dimension $$z=x^2+y^2$$, we may convert the data points into linearly separable data points.

![image]({{site.url}}/assets/SVM/figure4.png)

Let's demonstrate it by using one numerical example

**Example:**
**Consider following data points** 
* Positively Labelled Data Points:(3,1),(3,-1),(6,1),(6,-1)
* Negatively Labelled Data Points:(1,0),(0,1),(0,-1),(-1,0)

**Determine the equation of hyperplane that divides the above data points into two classes.
Then predict the class of data point (5,2).**

Solution: First plot the given points 

Positive Points: (3,1),(3,-1),(6,1),(6,-1)

Negative Points: (1,0),(0,1),(0,-1),(-1,0)

![image]({{site.url}}/assets/SVM/figure5.png)

Support vectors are

s1=(1,0),	 s2=(3,1), s3=(3,-1)		
    
Augment support vectors with bias = 1
    
    
s1=(1,0,1),	 s2=(3,1,1), s3=(3,-1,1)

Since there are three support vectors, we need to calculate three variables
Thus, three linear equations can be written as


 ![image]({{site.url}}/assets/SVM/figure6.png)
 
Because s1 belongs to the negative class and s2, s3, which are points belonging to the positive class, we wrote -1, 1 and 1 on the right side of the equation above.

After simplifying above equations, we get,

![image]({{site.url}}/assets/SVM/figure7.png)

solving these equations, we get

![image]({{site.url}}/assets/SVM/figure8.png)

Now, we can compute weight vector of the hyperplane as below,

![image]({{site.url}}/assets/SVM/figure9.png)

![image]({{site.url}}/assets/SVM/figure10.png)

Hence, equation of hyperplane that divides data points is 

X-2 = 0

Data point to be classified is (5,2)
Putting this data point is above equation we get,
	5-2=3
Thus the data point (5,2) belongs to +1 (Positively) class








```python

```
