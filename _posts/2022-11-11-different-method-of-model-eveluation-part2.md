---
title:  "Different Method of Model Evaluation(Part2)"
date:   2022-11-11 09:29:17 +0545
categories: Data Science
tags:
  - Model Evaluation
  - Model Selection
  - Model Validation
header:
  teaser: "assets/Model_evL/table.png"
  overlay_image: "assets/Model_evL/table.png"
toc: true
---
Previously, we wrote blogs on many machine learning algorithms as well as many other topics to help you broaden your knowledge. Please kindly visit our [site](https://dataqoil.com/blog/) and we would be glad if we got some feedback from you to improve our writing. To see some of them, you can follow the mentioned links.
* [Linear Regression](https://dataqoil.com/2022/04/21/fit-linear-regression-using-different-gradient-descent-algorithms/)

* [Logistic Regression](https://dataqoil.com/2020/08/11/writing-a-logistic-regression-class-from-scratch/)

* [K Medoids Clustering ](https://dataqoil.com/2022/02/04/k-medoids-clustering-in-python-from-scratch/)

* [DBSCAN Clustering](https://dataqoil.com/2022/08/05/dbscan-clustering-algorithm/)

* [K Means Clustering](https://dataqoil.com/2022/01/28/kmeans-clustering-in-python-from-scratch/)

Please click the following link to see our blog post on model evaluation for binary classification and clustering matrix.

* [Model Evaluation for Binary classification](https://dataqoil.com/2022/11/04/different-method-of-model-evaluation/)



Here, in this blog, we are going to discuss different types of model evaluation techniques for multi class classification and help which measure is suitable for your model.

## Introduction

Model evaluation is a technique for determining whether a model on test data is accurate. The test data consists of information that the model has never seen before. Model selection is a method for choosing the best model once each model has been assessed against the necessary standards. Multiple measures can be used to evaluate models. However, selecting the proper evaluation metric is important and frequently depends on the issue being resolved. The evaluator can find a suitable match between the problem statement and a metric by having a thorough understanding of a variety of metrics. There are different measure of model evaluation based up on weather it is balance classification problem or imbalance classification problem.

## Confusion Matrix

We must assess the performance of a classification algorithm before choosing it to tackle a problem. For calculating classification algorithm performance metrics, confusion matrices are frequently utilized. An N x N matrix called a confusion matrix is used to assess the effectiveness of a classification model, where N is the total number of target classes. In the matrix, the actual goal values are contrasted with those that the machine learning model anticipated. This gives us a comprehensive understanding of the effectiveness of our classification model and the types of mistakes it is committing. If there are only two classes then we call that classification problem as a binary classification problem however in multi-class classification problem there as more than two classes.

## Model evaluation technique for multi class classification problems

The confusion matrix is a NxN matrix if there are N classes. For instance, the confusion matrices for three classes are shown below.

|   |  A |  B | C  | 
|---|---|---|---|
| A  |  16 |  0 |  0 | 
| B  |  0 | 17  | 1  | 
|  C | 0  |  0 |  1 | 

Then we need to calculate **TP**, **FP**, **TN** and **FN** for each class separately. Let us discuss what does these term represents

**TP**: It represent actual and predicted both same.

**FP**: Sum of all entries in the row except TP.

**TN**: Sum of all entries in rows and columns except row and column of calculating class.

**FN**: Sum of all entries in the column except TP.

In above table let us calculate the respective values of TP, FP, TN, FN for three different class A, B, and C

**For Class A**: TP=2, FP=2, TN=5, FN:1

**For Class B**: TP=2, FP=1, TN=5, FN:2

**For Class C**: TP=3, FP=0, TN=7, FN:0

## Evaluation Metrics for Multi-class Classification

In multi-class classification, we first determine the accuracy of each class individually, and then we determine the accuracy of the weighted average.

### Recall

There are two methods for calculating Recall.

**Macro averaged recall**: Calculate each class's recall separately, then average them.

**Micro averaged recall**: Class-based calculations using true positives and false negatives to determine overall recall.

### Precision

Similarly, there are two different ways to calculate precision

**Macro averaged precision**:  Calculate precision for all classes individually and then average them.

**Micro averaged precision**: Class-based calculations Use the true positive and false positive rates to get the overall accuracy.

### F1-score

In the same way, there are two different ways to calculate F1-score.

**Macro averaged F1 Score**: Calculate f1 score of every class and then average them.
**Micro averaged F1 Score**: Take the harmonic mean of the micro-averaged precision and recall scores.

Let's clearly the above term using one example.

|   |  A |  B | C  | 
|---|---|---|---|
| A  |  16 |  0 |  0 | 
| B  |  0 | 17  | 1  | 
|  C | 0  |  0 |  1 |  

Solution:  We first calculate the TP, FP, FN, TN for each of the three classes,

**For class A**: 

**TP**: It represent actual and predicted both same = 16

**FP**: Sum of all entries in the row except TP = 0

**TN**: Sum of all entries in rows and columns except row and column of calculating class = 0

**FN**: Sum of all entries in the column except TP = 19

Now let's calculate Accuracy, Precision, Recall

**Accuracy:** It is indicated as follows and represents the model's proportion of accurate predictions.

      Accuracy = (TP + TN)/(TP + TN + FP + FN) = (16 + 19)/(16 +19 + 0 + 0) = 1
      
**Precision:** It is  percentage of predicted positives that are actually positive and is given by,

  Precision = TP/(TP + FP) = 16/ (16 + 0) = 1
  
**Recall:** It is the percentage of actual positives that are correctly classified by the model and is given as below,

  Recall = TP/(TP + FN) = 16/(16 + 0) = 1
  
**F1-Score:** It is the harmonic mean of recall and precision. It becomes high only when both precision and recall are high. This score is given by,

   F1-scoare = (2 * Recall * Precision)/(Recall + Precision) = (2 * 1 * 1)/(1 + 1) = 1
   
**For class B**:

**TP**: It represent actual and predicted both same = 17

**FP**: Sum of all entries in the row except TP = 1

**TN**: Sum of all entries in rows and columns except row and column of calculating class = 0

**FN**: Sum of all entries in the column except TP = 17

Now let's calculate Accuracy, Precision, Recall

**Accuracy:** It is indicated as follows and represents the model's proportion of accurate predictions.

      Accuracy = (TP + TN)/(TP + TN + FP + FN) = (17 + 17)/(17 +17 + 1 + 0) = 34/35 = 0.97
      
**Precision:** It is  percentage of predicted positives that are actually positive and is given by,

  Precision = TP/(TP + FP) = 17/ (17 + 1) = 17/18 = 0.94
  
**Recall:** It is the percentage of actual positives that are correctly classified by the model and is given as below,

  Recall = TP/(TP + FN) = 17/(17 + 0) = 1
  
**F1-Score:** It is the harmonic mean of recall and precision. It becomes high only when both precision and recall are high. This score is given by,

   F1-scoare = (2 * Recall * Precision)/(Recall + Precision) = (2 * 1 * 0.94)/(1.944) = 0.97
   
**For class C**:

**TP**: It represent actual and predicted both same = 1

**FP**: Sum of all entries in the row except TP = 0

**TN**: Sum of all entries in rows and columns except row and column of calculating class = 33

**FN**: Sum of all entries in the column except TP = 1

**Accuracy:** It is indicated as follows and represents the model's proportion of accurate predictions.

      Accuracy = (TP + TN)/(TP + TN + FP + FN) = (1 + 33)/(1 +33 + 1 + 0) = 0.97
      
**Precision:** It is  percentage of predicted positives that are actually positive and is given by,

  Precision = TP/(TP + FP) = 1/ (1 + 0) = 1
  
**Recall:** It is the percentage of actual positives that are correctly classified by the model and is given as below,

  Recall = TP/(TP + FN) = 1/(1 + 1) = 0.5
  
**F1-Score:** It is the harmonic mean of recall and precision. It becomes high only when both precision and recall are high. This score is given by,

   F1-scoare = (2 * Recall * Precision)/(Recall + Precision) = (2 * 1 * 0.5)/(1.5) = 0.666
   
Now let's calculate,

Weighted Average Accuracy = Accuracy of three classes/3 = (1+0.97+0.97)/3 = 0.98

Macro Average Precision = Precision of three classes/3 = (1+ 0.944 +1)/3 = 0.98

Macro Average Recall = Recall of three classes / 3 = ( 1+ 1 + 0.5)/3 = 0.833

Macro Average F1 score = F1 score of individual class /3 = (1 + 0.97 + 0.666)/3 = 0.88

Micro Average precision = (Tpa + Tpb + Tpc)/(Tpa + Tpb + Tpc + Fpa + Fpb + Fpc) = 0.97

Micro Average Recall = (Tpa + Tpb + Tpc)/(Tpa + Tpb + Tpc + FNa + FNb + FNc) = 0.97

Micro Average F1-score = (2* 0.97 * 0.97)/(0.97 + 0.97) = 0.97
   














```python

```
