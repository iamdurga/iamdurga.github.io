---
title:  "Naive Bayes From Scratch"
date:   2022-11-18 09:29:17 +0545
categories: Machine Learning
tags:
  - Naive Bayes
  - Machine Learning
  - Classification
header:
  teaser: "assets/Model_evL/table.png"
  overlay_image: "assets/Model_evL/table.png"
toc: true
---
Previously, we wrote blogs on many machine learning algorithms(Classification, Predication) as well as many other topics to help you sharpen your knowledge of how machine work. Please kindly visit our [site](https://dataqoil.com/blog/) and we would be happy if we got some feedback from you to improve our writing. To see some of them, you can follow the mentioned links.

* [Linear Regression](https://dataqoil.com/2022/04/21/fit-linear-regression-using-different-gradient-descent-algorithms/)

* [Logistic Regression](https://dataqoil.com/2020/08/11/writing-a-logistic-regression-class-from-scratch/)

* [K Medoids Clustering ](https://dataqoil.com/2022/02/04/k-medoids-clustering-in-python-from-scratch/)

* [DBSCAN Clustering](https://dataqoil.com/2022/08/05/dbscan-clustering-algorithm/)

* [K Means Clustering](https://dataqoil.com/2022/01/28/kmeans-clustering-in-python-from-scratch/)

In this blog, we are going to do Naive Bayes by scratch. We can easily fit our own code instead of fitting our Naive Bayes model from the library; however, writing code from scratch really helps you appreciate how algorithms work. We already talked about how mathematically naive Bayes works. If you want to see how Naive Bayes works mathematically, click on the following link.

* [Mathematics Behind Naive Bayes](https://dataqoil.com/2022/10/21/1253/)

# Bayes Theorem

Naive Bayes work on the basis of `Bayes Theorem`

$$P(A\mid B)=\frac {P(B\mid A) \cdot P(A)}{P(B)}$$

Where, P(A/B) = Posterior Probability
  
       P(B/A) = Conditional Probability
       
       P(A) = Prior Probability
       
       P(B) = Marginal Probability. 
       
  Here, P(B) is constant for all values and hence does not contribute much to classifying the dataset, so we neglect that term while doing calculations.



# Import Necessary Module


```python
import pandas as pd 

```

# Data Load

Here we use diabetes data. If you are interested in obtaining a data set, please visit [link]. (https://www.kaggle.com/datasets/uciml/pima-indians-diabetes-database) Talking about the dataset, it predicts whether a patient has diabetes or not on the basis of measurements (pregnancys,glucosee,blood pressuree,skin thicknesss,insulinn, BMI,diabetes pedigree functionn,agee).


```python
df = pd.read_csv('diabetes.csv')
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Pregnancies</th>
      <th>Glucose</th>
      <th>BloodPressure</th>
      <th>SkinThickness</th>
      <th>Insulin</th>
      <th>BMI</th>
      <th>DiabetesPedigreeFunction</th>
      <th>Age</th>
      <th>Outcome</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6</td>
      <td>148</td>
      <td>72</td>
      <td>35</td>
      <td>0</td>
      <td>33.6</td>
      <td>0.627</td>
      <td>50</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>85</td>
      <td>66</td>
      <td>29</td>
      <td>0</td>
      <td>26.6</td>
      <td>0.351</td>
      <td>31</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>183</td>
      <td>64</td>
      <td>0</td>
      <td>0</td>
      <td>23.3</td>
      <td>0.672</td>
      <td>32</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>89</td>
      <td>66</td>
      <td>23</td>
      <td>94</td>
      <td>28.1</td>
      <td>0.167</td>
      <td>21</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>137</td>
      <td>40</td>
      <td>35</td>
      <td>168</td>
      <td>43.1</td>
      <td>2.288</td>
      <td>33</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



# Convert Continuous Data to Categorical Data 

For classification tasks, we always need data in categorical format, but our available data is in continuous type. So our first task is to convert the given data into categorical data while also dealing with missing values. To change the given data into categorical format, we use the "pandas cut function." which work in the following manner:

`cut(array, bins, level)`

If we do not provide the bins size it automatically create the bins size in this way,

M = maximum value of array

m = minimum value of array

R = M - m

bins = round(sqrt(R)) 

But, in our care, we already provided the bin size, so it must first find the maximum value and divide that value by the number of bins, and then categorize our dataset according to the level we have provided.


```python
labels = ['lower','medium','higher']
for i in df.columns[:-1]: 
    mean = df[i].mean() 
    df[i] = df[i].replace(0,mean) 
    df[i] = pd.cut(df[i],bins=len(labels),labels=labels)
    
    
```

# Count Function
 
 The below count function simply counts how much data there is according to class and category, respectively.


```python
def count(df,colname,label,target):
    rule = (df[colname] == label) & (df['Outcome'] == target) 
    return len(df[rule])
```


```python
predicted = []
```


```python
probabilities = {0:{},1:{}}
```

# Split Data into Train and Test Set

We use 70% of the data without any random process in this data splitting process; however, this is not a good approach because it may be affected by bias at times, so I strongly recommend you use the k-folds approach or any other random splitting process. 


```python
train_percent = 70
train_len = int((train_percent*len(df))/100)
train_X = df.iloc[:train_len,:]
test_X = df.iloc[train_len+1:,:-1]
test_y = df.iloc[train_len+1:,-1]
```

# Prior probability

Now, let's calculate prior probability by using following formula,

 P(Outcome => 0) = Count(0)/Total Number of data
 
P(Outcome => 1) = Count(1)/Total Number of data 


```python
total_0 = count(train_X,'Outcome',0,0)
total_1 = count(train_X,'Outcome',1,1)
    
prior_prob_0 = total_0/len(train_X)
prior_prob_1 = total_1/len(train_X)
```

# Conditional Probability
In Bayes Theorem there is another kind of probability which is known as conditional probability. Lets calculate it using following formula.

Conditional-probability = P(Count of Category/Count of 0)

Conditional-probability = P(Count of Category/Count of 1)



```python
for col in train_X.columns[:-1]:
        probabilities[0][col] = {}
        probabilities[1][col] = {}
        
        for category in labels:
            total_ct_0 = count(train_X,col,category,0)
            total_ct_1 = count(train_X,col,category,1)
            
            probabilities[0][col][category] = total_ct_0 / total_0
            probabilities[1][col][category] = total_ct_1 / total_1
```

# Posterior probability

Finally, 

Posterior Probability = Conditional Probability * Prior probability


```python
for row in range(0,len(test_X)):
        prod_0 = prior_prob_0
        prod_1 = prior_prob_1
        for feature in test_X.columns:
            prod_0 *= probabilities[0][feature][test_X[feature].iloc[row]] 
            prod_1 *= probabilities[1][feature][test_X[feature].iloc[row]] 
            
        
        
        if prod_0 > prod_1:
            predicted.append(0)

        else:
            predicted.append(1)
            

```

# Which is the class for the given dataset?


```python
have_diabetes = 0
do_not_have = 0

for i in predicted:
    if i == 0:
        do_not_have +=1 
    else:
        have_diabetes += 1
print(have_diabetes)
print(do_not_have)
print("Final predication for given dataset is patient do not have diabetes")
```

    79
    151
    Final predication for given dataset is patient do not have diabetes
    

# The Given Classification Model's Accuracy 


```python
tp,tn,fp,fn = 0,0,0,0
for j in range(0,len(predicted)):
    if predicted[j] == 0:
        #print(test_y.iloc[j])
        if test_y.iloc[j] == 0:
            tp += 1
        else:
            fp += 1
    else:
        if test_y.iloc[j] == 1:
            tn += 1
        else:
            fn += 1
```


```python
++print('Accuracy for training length '+str(train_percent)+'% : ',((tp+tn)/len(test_y))*100)
```

    Accuracy for training length 70% :  80.0
    
