---
title:  "Naive Bayes From Scratch"
date:   2022-11-18 09:29:17 +0545
categories: Machine Learning
tags:
  - Naive Bayes
  - Machine Learning
  - Classification
header:
  teaser: "assets/outlier/outlier.png"
  overlay_image: "assets/outlier/outlier.png"
toc: true
---
Previously, we wrote blogs on many machine learning algorithms(Classification, Predication) as well as many other topics to help you sharpen your knowledge of how machine work. Please kindly visit our [site](https://dataqoil.com/blog/) and we would be happy if we got some feedback from you to improve our writing. To see some of them, you can follow the mentioned links.

* [Linear Regression](https://dataqoil.com/2022/04/21/fit-linear-regression-using-different-gradient-descent-algorithms/)

* [Logistic Regression](https://dataqoil.com/2020/08/11/writing-a-logistic-regression-class-from-scratch/)

* [K Medoids Clustering ](https://dataqoil.com/2022/02/04/k-medoids-clustering-in-python-from-scratch/)

* [DBSCAN Clustering](https://dataqoil.com/2022/08/05/dbscan-clustering-algorithm/)

* [K Means Clustering](https://dataqoil.com/2022/01/28/kmeans-clustering-in-python-from-scratch/)

In this blog, we are going to discuss what outliers are as well as various outlier detection measures.

Image that you are a transactions auditor in credit card company. To protect your customers from credit card fraud, you pay special attention to card usages that are rather different from typical cases. For example, if a purchase amount is much bigger than usual for a card owner, and if the purchases occurs far from the owner's resident city, then the purchase is suspicious. You want to detect such transactions as soon as they occur and contact the card owner for verification. This is common practice in many credit card companies. 

Most credit card transactions are normal. However, if a credit card is stolen, its transaction pattern usually changes dramatically. The locations of purchases and the items purchased are often very different from those that of authentic card owner and other customers. An essential idea behind credit card fraud detection is to identify those transactions that are very different from normal. Hence outliers detection is the process of finding data objects with behaviors that are very different from expectation. 

# What are Outliers?
Assume that a given statistical process is used to generate a set of data objects. An outliers is a data object that deviates significantly from rest of the objects, as if it were generated by a different mechanism. 

![image]({{site.url}}/assets/outlier/outlier.png)

In figure most of object follow a roughly a Gaussian distribution. However, the objects in outliers are significantly different. It is unlikely that they follow the same distribution as the objects in the data set. 

# Types of Outliers

In general outliers can be classified into three categories, namely global outliers, contextual outliers, and collective outliers. let's examine  each of these categories.

## Global Outliers
In a given data set, a data object is global outliers if it deviates significantly from the rest of the data set. Global outliers are sometimes called point anomalies, and are the simplest type of outliers. Most outliers detection method aimed at finding global outliers. Consider the points in above figure. The points in region outlier significantly deviate from the rest of the data set, and are example of global outliers.

Global outliers detection is important in many applications. Consider intrusion detection in computer networks, foe example. If the communication behavior of a computer is very different from the normal patterns(large number of package is broad-cast in a short time), this behavior may be consider as global outlier and the corresponding computer is suspected victim of hacking.

## Contextual Outliers

"The temperature today is 28^o c. Is it exceptional?". It depends, for example, on the time and location! If it is winter in Nepal, yes, it is an outlier. If it is a summer day in Nepal, them it is normal. Unlike global outlier detection, in this case, whether or not today's temperature value is an outlier depends on the context the date, the location, and possibly some other factors. 

In a given data set, data object is a contextual outliers if it deviates significantly with respect to a specific context of the object. Contextual outliers are also known as conditional outliers because they are conditional on the selected context.
Generally, in contextual outliers detection, the attributes of the data objects in the question are divided into two groups,

* Contextual Attributes: The contextual attributes of a data object define the object's context, In the temperature example, the contextual attributes may be date and location.

* Behavioral Attributes: These define the object's characteristic, and are used to evaluate whether the object is an outlier in the context to which it belongs. In the temperature example, the behavioral attributes may be the temperature, humidity and pressure.

## Collective Outliers

Suppose you are a supply -chain manager of AllElectronics. You handle thousand of orders and shipments every day. If the shipment of an order is delayed, it may not be considered an outliers because, statistically, delays on a single day. However you have to pay attention if 100 orders are delayed on a single day. Those 100 orders as a whole form an outliers, although each of them may not be consider as outlier if considered individually.

Given a data set, a subset of data objects from a collective outliers if the objects as a whole deviate significantly from the entire data set. Importantly, the individual data objects may not be outliers.

![image]({{site.url}}/assets/outlier/outliers2.png)

In figure the black objects as a whole form a collective outliers because the density of those objects is much higher than the rest in the data set. However, every black object individually is not an outlier with respect to the whole data set. Collective outlier detection has many important applications. For example, in intrusion detection,a denial-of-service package from one computer to another is consider normal, and not an outlier at all. However, if several computers keep sending denial-of-service packages to each other, they as a whole should be considered as a collective outlier. The computers involved may be suspected of being compromised by an attack.

# Outlier Detection Methods

There are many outlier detection method in literature and in practice. Here, we present two orthogonal ways to categorize outlier detection methods. First, we categorize outlier detection methods according to whether the sample of data for analysis is given with domain expert- provided labels that can be used to build an outliers detection model. Second, we divide methods into groups according to their assumptions regarding normal objects versus outliers.

**Supervised Methods** Supervised methods model data normality and abnormality. Domain experts examine and label a sample of the underlying data. Outliers detection can then modeled as a classification problem. The task is to learn a classifier that can recognize outliers. The sample is used for training and testing. In some applications, the experts may label just the normal objects, and any other objects not matching the model of normal objects are reported as outliers.

**Unsupervised Methods** In some application scenarios, objects labeled as "normal" or "outlier" are not available. Thus, an unsupervised learning method has to be used. Unsupervised method make a assumption normal objects follow a pattern far more frequently than outliers. Normal object do not have to fall into one group sharing high similarity. Instead, they can form multiple groups, where each group has distinct features. However, an outlier is expected to occur far away in feature space from any of those groups of normal objects.

**Semi-Supervised Methods** In many example, although obtaining some labeled examples is feasible, the number of such labeled example is often small. We may encounter cases where only a small set of the normal and/or outlier objects are labeled, but most of the data are unlabeled. Semi-supervised outlier detection methods were developed to tackle such scenarios.

Semi supervised outlier detection methods can be regarded as  applications of semi-supervised learning methods. Foe example, when some labeled normal objects are available, we can use them, together with unlabeled objects that are close by, to train a model for normal objects. The model of normal objects then are classified as outliers.

**Statistical Method** Statistical methods make assumptions of data normality. They assume that normal data objects are generated by a statistical model, and that data not following the model are outliers. Consider in above first figure the data points except for those in region outliers fit a Gaussian distribution, where for a location x in the data space gives the probability density at x. Thus, Gaussian distribution can be used to model the normal data, that is most of the data points in the data set. For each objects y in region **outlirs**, we can estimate Gaussian distribution for y in outliers, the probability that this points fits the Gaussian distribution. Because of Gaussian distribution for y in outliers is unlikely generated by the Gaussian model, and thus is an outlir.

>>The effectiveness of statistical methods highly depends on whether the assumptions made for the statistical model hold true for the given data. There are many kind of statistical models. For example, the statics methods used in the methods may be parametric or nonparametric.

**Proximity-Based Methods** Proximity-based methods assume that an object is an outliers if the nearest neighbors of the object are far away in feature space, that is, the proximity of the object to its neighbors significantly deviates from the proximity of most of the other objects to their neighbors in the same data set. Consider the object in above first figure. If we model the proximity of an object using its three nearest neighbors, then the objects in region outlier are substantially different from other objects in the data set. For the two objects in outlier, their second and third nearest neighbors are dramatically more remote than those of any other objects. Therefore we can label the objects in region outlier as outliers based on proximity.

>> The effectiveness of proximity-based methods relies heavily on the proximity measure used. In some applications, such measures cannot be easily obtained. Moreover, proximity-based methods often have difficulty in detecting a group of outliers if the outliers are close to one another.


**Clustering-Based Methods** Clustering-based methods assume that the normal data objects belong to large and dense cluster, whereas outliers belong to small or sparse clusters, or do not belong to any clusters.

In above figure first, there are two clusters. Cluster c1 containing all the points in the data set except for those in region outliers. Cluster C2 is tiny  containing just two points in outlier. Cluster C1 is large in comparison to C2. Therefore, a clustering-based methods asserts that the two objects in outlier are outliers.

>> Clustering is an expensive data mining operation. A straightforward adaption of a clustering method for outliers detection can be very costly, and thus does not scale up well for large data sets. 

# Challenges of Outlier Detection

Outlier detection is useful in many applications yet faces many challenges such as the following,

**Modeling Normal Objects and Outliers Effectively** Outlier detection quality highly depends on the modeling of normal(nonoutlier) objects and outliers. Often, building a comprehensive model for data normality is very challenging, if not impossible. This is partly because it is hard to enumerate all possible normal behaviors in an application.

**Application-Specific outlier detection** Technically, choosing the similarity/distance measure and the relationship model to describe data objects in critical in outlier detection. Unfortunately, such choice are often application-dependent. Different applications may have very different requirements. For example, in clinic data analysis,a small deviation may be important enough to justify an outliers. In contract, in marketing analysis, objects are often subject to larger fluctuations, and consequently a substantially larger deviation is needed to justify an outliers. 

**Handeling Noise in Outlier Detection** As mention earlier, outliers are different from noise. It is also well known that the quality of real data sets tends to be poor. Noise often unavoidably exists in data collected in many applications. Noise may be present as deviation in attribute values or even as a missing values. Low data quality and the presence of noise bring a huge challenge to outlier detection. They can distort the data, blurring the distinction between the normal object and outliers.

**Understandability** In some application scenarios, a user may want to not only detect outliers, but also understand why the detected objects are outliers. To meet the understandability requirement, an outlier detection method has to provide some justification of the detection. For example, a statistical method can be used to justify the degree to which an object may be an outlier based on the likelihood that the object was generated by the some mechanism that generated the majority of the data.  The smaller the likelihood, the more unlikely the object was generated by the same mechanism, and the more likely the object is outlier.



References
* https://www.google.com/search?q=images+of+collective+outliers&tbm=isch&ved=2ahUKEwjXtu2hscj7AhVqjtgFHcDnDVsQ2-cCegQIABAA&oq=images+of+collective+outliers&gs_lcp=CgNpbWcQAzoFCAAQgAQ6BAgjECc6BAgAEEM6BwgAELEDEEM6CAgAEIAEELEDOgYIABAFEB46BggAEAgQHlCiFViQUWDdV2gAcAB4AIABmwGIAZobkgEEMC4zMJgBAKABAaoBC2d3cy13aXotaW1nwAEB&sclient=img&ei=wTWAY5fSDOqc4t4PwM-32AU&bih=715&biw=1496&client=opera&hs=34n#imgrc=Ziab4kNZBWW6-M

* https://www.google.com/search?q=images+of+outliers&tbm=isch&ved=2ahUKEwi2ocKYscj7AhVJj9gFHU7tAsgQ2-cCegQIABAA&oq=images+of+outliers&gs_lcp=CgNpbWcQAzIFCAAQgAQ6BAgjECc6BwgjEOoCECc6CAgAEIAEELEDOgcIABCxAxBDUJcEWLU9YMlCaAFwAHgEgAGWAYgBhiWSAQQwLjQxmAEAoAEBqgELZ3dzLXdpei1pbWewAQrAAQE&sclient=img&ei=rTWAY_aWJsme4t4PztqLwAw&bih=715&biw=1496&client=opera&hs=34n#imgrc=GFrAVh4xlm5RUM

* Book(Data Mining Concept and Technology)





```python

```