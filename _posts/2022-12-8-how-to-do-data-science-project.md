---
title:  "How to do Data Science Project"
date:   2022-12-1 07:29:17 +0545
categories: Data Science
tags:
  - Outliers
  - Data Science
  - Accuracy
header:
  teaser: "assets/outlier/outlier.png"
  overlay_image: "assets/outlier/outlier.png"
toc: true
---

Data science project can be a challenging but rewarding process. By following the steps we can use in this blog, you can work through the project in an organized and effective way, and ultimately arrive at a solution to your problem.

Previously, we wrote blogs on many machine learning algorithms (Classification, Predication) as well as many other topics to help you sharpen your knowledge of how machine work. Please kindly visit our [site](https://dataqoil.com/blog/) and we would be happy if we got some feedback from you to improve our writing. To see some of them, you can follow the mentioned links.

* [Linear Regression](https://dataqoil.com/2022/04/21/fit-linear-regression-using-different-gradient-descent-algorithms/)

* [Logistic Regression](https://dataqoil.com/2020/08/11/writing-a-logistic-regression-class-from-scratch/)

* [K Medoids Clustering ](https://dataqoil.com/2022/02/04/k-medoids-clustering-in-python-from-scratch/)

* [DBSCAN Clustering](https://dataqoil.com/2022/08/05/dbscan-clustering-algorithm/)

* [K Means Clustering](https://dataqoil.com/2022/01/28/kmeans-clustering-in-python-from-scratch/)


Dataset is from Kaggle. This is the bank dataset for Credit evaluation whether to grant loan or not. 

https://www.kaggle.com/datasets/brycecf/give-me-some-credit-dataset

<font color= red> Disclaimer: This exercise is targeted to audience of all levels including the beginners, so we will be using simple methods, not advanced functions. </font>

Some of concept in this blog are borrowed from lecture note of [Data Scientist Nirmal Budhathoki](https://www.linkedin.com/in/nirmal-budhathoki/).

**Our goal:** </br>
For this notebook, we want to perform Exploratory Data Analysis (EDA), learn some data cleaning techniques, handling missing values and etc.

**Business Understanding:** For the banks, customers going to delinquent or default is a bad news. These are people who are not able to pay their credit. The defaulted loans goes to collection team. This is a loss for bank. Therefore, if we can predict whether a customer will default in next 90 days, then bank can take precautionary actions like interest relief, lower payment plan, extending payoff time etc. 





## Importing Required Libraries


```python
import pandas as pd
import numpy as np
import joblib
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline
from IPython.display import Image
import warnings
from sklearn.linear_model import LogisticRegression
from sklearn.ensemble import RandomForestClassifier
from sklearn.preprocessing import StandardScaler
from sklearn.model_selection import train_test_split
from sklearn import metrics
from sklearn.metrics import confusion_matrix, classification_report, precision_recall_curve,recall_score
warnings.filterwarnings('ignore')

sns.set(rc={'figure.figsize':(10,8)})
```

**Data Understanding:** </br>
Loading Data - We will only load training data for this exercise. You have to download the cs-training.csv from the above link and upload the file into you Google Drive. You can also use the API to read it from kaggle directly. More information on API in this link: https://www.kaggle.com/general/74235


```python
## For now we will load from the drive
dataset = pd.read_csv('cs-training.csv')

```


```python
## Checking top 5 rows
dataset.head()
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
      <th>Unnamed: 0</th>
      <th>SeriousDlqin2yrs</th>
      <th>RevolvingUtilizationOfUnsecuredLines</th>
      <th>age</th>
      <th>NumberOfTime30-59DaysPastDueNotWorse</th>
      <th>DebtRatio</th>
      <th>MonthlyIncome</th>
      <th>NumberOfOpenCreditLinesAndLoans</th>
      <th>NumberOfTimes90DaysLate</th>
      <th>NumberRealEstateLoansOrLines</th>
      <th>NumberOfTime60-89DaysPastDueNotWorse</th>
      <th>NumberOfDependents</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>0.766127</td>
      <td>45</td>
      <td>2</td>
      <td>0.802982</td>
      <td>9120.0</td>
      <td>13</td>
      <td>0</td>
      <td>6</td>
      <td>0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0</td>
      <td>0.957151</td>
      <td>40</td>
      <td>0</td>
      <td>0.121876</td>
      <td>2600.0</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0</td>
      <td>0.658180</td>
      <td>38</td>
      <td>1</td>
      <td>0.085113</td>
      <td>3042.0</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0</td>
      <td>0.233810</td>
      <td>30</td>
      <td>0</td>
      <td>0.036050</td>
      <td>3300.0</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0</td>
      <td>0.907239</td>
      <td>49</td>
      <td>1</td>
      <td>0.024926</td>
      <td>63588.0</td>
      <td>7</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>



##  Checking the shape of Dataframe


```python

dataset.shape
```




    (150000, 12)



# Check the data types


```python
dataset.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 150000 entries, 0 to 149999
    Data columns (total 12 columns):
     #   Column                                Non-Null Count   Dtype  
    ---  ------                                --------------   -----  
     0   Unnamed: 0                            150000 non-null  int64  
     1   SeriousDlqin2yrs                      150000 non-null  int64  
     2   RevolvingUtilizationOfUnsecuredLines  150000 non-null  float64
     3   age                                   150000 non-null  int64  
     4   NumberOfTime30-59DaysPastDueNotWorse  150000 non-null  int64  
     5   DebtRatio                             150000 non-null  float64
     6   MonthlyIncome                         120269 non-null  float64
     7   NumberOfOpenCreditLinesAndLoans       150000 non-null  int64  
     8   NumberOfTimes90DaysLate               150000 non-null  int64  
     9   NumberRealEstateLoansOrLines          150000 non-null  int64  
     10  NumberOfTime60-89DaysPastDueNotWorse  150000 non-null  int64  
     11  NumberOfDependents                    146076 non-null  float64
    dtypes: float64(4), int64(8)
    memory usage: 13.7 MB
    

Observation: All Columns are Numeric, either int or float

# Check for Missing Values


```python
dataset.isnull().sum()
```




    Unnamed: 0                                  0
    SeriousDlqin2yrs                            0
    RevolvingUtilizationOfUnsecuredLines        0
    age                                         0
    NumberOfTime30-59DaysPastDueNotWorse        0
    DebtRatio                                   0
    MonthlyIncome                           29731
    NumberOfOpenCreditLinesAndLoans             0
    NumberOfTimes90DaysLate                     0
    NumberRealEstateLoansOrLines                0
    NumberOfTime60-89DaysPastDueNotWorse        0
    NumberOfDependents                       3924
    dtype: int64



Observation: There are two attributes missing some values, lets see the percentage missing.


```python
 dataset.isnull().sum() * 100 / len(df)
```




    Unnamed: 0                               0.000000
    SeriousDlqin2yrs                         0.000000
    RevolvingUtilizationOfUnsecuredLines     0.000000
    age                                      0.000000
    NumberOfTime30-59DaysPastDueNotWorse     0.000000
    DebtRatio                                0.000000
    MonthlyIncome                           19.820667
    NumberOfOpenCreditLinesAndLoans          0.000000
    NumberOfTimes90DaysLate                  0.000000
    NumberRealEstateLoansOrLines             0.000000
    NumberOfTime60-89DaysPastDueNotWorse     0.000000
    NumberOfDependents                       2.616000
    dtype: float64




```python
dataset.nunique()
```




    Unnamed: 0                              150000
    SeriousDlqin2yrs                             2
    RevolvingUtilizationOfUnsecuredLines    125728
    age                                         86
    NumberOfTime30-59DaysPastDueNotWorse        16
    DebtRatio                               114194
    MonthlyIncome                            13594
    NumberOfOpenCreditLinesAndLoans             58
    NumberOfTimes90DaysLate                     19
    NumberRealEstateLoansOrLines                28
    NumberOfTime60-89DaysPastDueNotWorse        13
    NumberOfDependents                          13
    dtype: int64




```python
dataset.duplicated().value_counts()
```




    False    150000
    dtype: int64




```python
dataset['Unnamed: 0'].describe()
```




    count    150000.000000
    mean      75000.500000
    std       43301.414527
    min           1.000000
    25%       37500.750000
    50%       75000.500000
    75%      112500.250000
    max      150000.000000
    Name: Unnamed: 0, dtype: float64



Observation: This is just the index field or unique row number , which will not add any value to the modeling. so lets drop it.


```python
dataset.drop(columns = ['Unnamed: 0'], axis=1, inplace = True)
```


```python
dataset.duplicated().value_counts()
```




    False    149391
    True        609
    dtype: int64




```python
dataset = dataset.drop_duplicates()
```


```python
dataset.shape
```




    (149391, 11)



### Now lets see how our labels are distributed


```python
dataset['SeriousDlqin2yrs'].value_counts(normalize= True)
```




    0    0.933001
    1    0.066999
    Name: SeriousDlqin2yrs, dtype: float64




```python
df['SeriousDlqin2yrs'].value_counts(normalize=True).plot(kind='barh');

```


    
![image]({{site.url}}/assets/project/output_25_0.png)
    


Observation: We have roughly 93% NOT Delinquient, and only 7% customers are delinquent. This is classic example of CLASS IMBALANCE.

### UNIVARIATE ANALYSIS - ONE VARIABLE AT A TIME


```python
## UNIVARIATE ANALYSIS
# Creating histograms
dataset.hist(figsize=(14,14))
plt.show()
```


    
![image]({{site.url}}/assets/project/output_28_0.png)
    



```python
dataset['RevolvingUtilizationOfUnsecuredLines'].describe()
```




    count    149391.000000
    mean          6.071087
    std         250.263672
    min           0.000000
    25%           0.030132
    50%           0.154235
    75%           0.556494
    max       50708.000000
    Name: RevolvingUtilizationOfUnsecuredLines, dtype: float64



Observation: The max value is questionable. The revolving utilization means ratio of credit balance/ credit limit, which should always be 0 to 1, since it is ratio. Now lets see how many of such values we have. 


```python
len(dataset[(dataset['RevolvingUtilizationOfUnsecuredLines']>1)])
```




    3321




```python
## Lets see distribution of values that are <= 1
dataset_revUtil_less_than_one= dataset.loc[dataset['RevolvingUtilizationOfUnsecuredLines'] <=1]
sns.displot(data= dataset_revUtil_less_than_one, x= "RevolvingUtilizationOfUnsecuredLines", kde= True);
```


    
![image]({{site.url}}/assets/project/output_32_0.png)
    



```python
## since there are 3321 values have issues, its better to treat them as Nulls first and then impute, we can try ffill
dataset['RevolvingUtilizationOfUnsecuredLines'] = dataset['RevolvingUtilizationOfUnsecuredLines'].map(lambda x: np.NaN if x >1 else x)
dataset['RevolvingUtilizationOfUnsecuredLines'].fillna(method='ffill', inplace=True)
```


```python
dataset['RevolvingUtilizationOfUnsecuredLines'].describe()
```




    count    149391.000000
    mean          6.071087
    std         250.263672
    min           0.000000
    25%           0.030132
    50%           0.154235
    75%           0.556494
    max       50708.000000
    Name: RevolvingUtilizationOfUnsecuredLines, dtype: float64




```python
dataset['RevolvingUtilizationOfUnsecuredLines'].plot.hist();
```


    
![image]({{site.url}}/assets/project/output_35_0.png)
    


We are able to change all the data into 0 to 1 range.

## Age


```python
dataset['age'].describe()
```




    count    149391.000000
    mean         52.306237
    std          14.725962
    min           0.000000
    25%          41.000000
    50%          52.000000
    75%          63.000000
    max         109.000000
    Name: age, dtype: float64




```python
sns.displot(data = dataset['age'], kde= True);
```


    
![image]({{site.url}}/assets/project/output_39_0.png)
    



```python
sns.boxplot(data= dataset['age'])
```




    <AxesSubplot:>




    
![image]({{site.url}}/assets/project/output_40_1.png)
    


## Using Z Score for Outlier Analysis


```python
dataset['age_zscore'] = (dataset['age'] - dataset['age'].mean())/dataset['age'].std(ddof=0)
dataset.head()
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
      <th>SeriousDlqin2yrs</th>
      <th>RevolvingUtilizationOfUnsecuredLines</th>
      <th>age</th>
      <th>NumberOfTime30-59DaysPastDueNotWorse</th>
      <th>DebtRatio</th>
      <th>MonthlyIncome</th>
      <th>NumberOfOpenCreditLinesAndLoans</th>
      <th>NumberOfTimes90DaysLate</th>
      <th>NumberRealEstateLoansOrLines</th>
      <th>NumberOfTime60-89DaysPastDueNotWorse</th>
      <th>NumberOfDependents</th>
      <th>age_zscore</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0.766127</td>
      <td>45</td>
      <td>2</td>
      <td>0.802982</td>
      <td>9120.0</td>
      <td>13</td>
      <td>0</td>
      <td>6</td>
      <td>0</td>
      <td>2.0</td>
      <td>-0.496148</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>0.957151</td>
      <td>40</td>
      <td>0</td>
      <td>0.121876</td>
      <td>2600.0</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
      <td>-0.835686</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>0.658180</td>
      <td>38</td>
      <td>1</td>
      <td>0.085113</td>
      <td>3042.0</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>-0.971501</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0.233810</td>
      <td>30</td>
      <td>0</td>
      <td>0.036050</td>
      <td>3300.0</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>-1.514761</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>0.907239</td>
      <td>49</td>
      <td>1</td>
      <td>0.024926</td>
      <td>63588.0</td>
      <td>7</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0.0</td>
      <td>-0.224518</td>
    </tr>
  </tbody>
</table>
</div>




```python
dataset[(dataset['age_zscore'] > 3) | (df['age_zscore'] < -3)].shape
```




    (45, 12)




```python
condition= dataset[(dataset['age_zscore'] > 3) | (dataset['age_zscore'] < -3)]
```


```python
dataset.drop(condition.index, inplace= True)
```


```python
df.shape
```




    (149346, 12)




```python
sns.boxplot(data= dataset['age'])
```




    <AxesSubplot:>




    
![image]({{site.url}}/assets/project/output_47_1.png)
    



```python
dataset['age'].describe()
```




    count    149346.000000
    mean         52.292689
    std          14.705177
    min          21.000000
    25%          41.000000
    50%          52.000000
    75%          63.000000
    max          96.000000
    Name: age, dtype: float64



##  DEBT RATIO
Debt to income ratio or debt to assets ratio. This is typically 0 to 1, but sometimes it can be higher than 1, meaning person has more debt than income or assets. 


```python
dataset['DebtRatio'].describe()
```




    count    149346.000000
    mean        354.501212
    std        2042.133602
    min           0.000000
    25%           0.177484
    50%           0.368253
    75%           0.875062
    max      329664.000000
    Name: DebtRatio, dtype: float64




```python
dataset2=dataset[dataset['DebtRatio']>1]['DebtRatio']
dataset2
```




    6         5710.000000
    8           46.000000
    14         477.000000
    16        2058.000000
    25           1.595253
                 ...     
    149976      60.000000
    149977     349.000000
    149984      25.000000
    149992    4132.000000
    149997    3870.000000
    Name: DebtRatio, Length: 35115, dtype: float64




```python
dataset2.describe()
```




    count     35115.000000
    mean       1506.721853
    std        4000.145613
    min           1.000500
    25%          42.000000
    50%         908.500000
    75%        2211.000000
    max      329664.000000
    Name: DebtRatio, dtype: float64




```python
dataset2.plot.box()
```




    <AxesSubplot:>




    
![image]({{site.url}}/assets/project/output_53_1.png)
    


Lets make an assumption that Debt to Income ratio should be 0 to 1. Since there are 35,122 data points with Debt ratio higher than 1, instead of dropping them we can make assumption that number with higher than 1 are 100 % Debt ratio so fill them with 1. 


```python
dataset['DebtRatio']= dataset['DebtRatio'].apply(lambda x: 1 if x>1 else x)
dataset['DebtRatio']
```




    0         0.802982
    1         0.121876
    2         0.085113
    3         0.036050
    4         0.024926
                ...   
    149995    0.225131
    149996    0.716562
    149997    1.000000
    149998    0.000000
    149999    0.249908
    Name: DebtRatio, Length: 149346, dtype: float64




```python
df['DebtRatio'].plot.hist()
```




    <AxesSubplot:ylabel='Frequency'>




    
![image]({{site.url}}/assets/project/output_56_1.png)
    


## INCOME


```python
dataset.MonthlyIncome.describe()
```




    count    1.201470e+05
    mean     6.675649e+03
    std      1.439086e+04
    min      0.000000e+00
    25%      3.400000e+03
    50%      5.400000e+03
    75%      8.250000e+03
    max      3.008750e+06
    Name: MonthlyIncome, dtype: float64




```python
dataset.MonthlyIncome.isnull().sum()
```




    29199




```python
dataset.MonthlyIncome.median()
```




    5400.0




```python
dataset['MonthlyIncome'].fillna(dataset['MonthlyIncome'].median(),inplace=True)
```


```python
dataset.MonthlyIncome.plot.box()
```




    <AxesSubplot:>




    
![image]({{site.url}}/assets/project/output_62_1.png)
    



```python
dataset['MonthlyIncome_zscore'] = (dataset['MonthlyIncome'] - dataset['MonthlyIncome'].mean())/dataset['MonthlyIncome'].std(ddof=0)
```


```python
condition= dataset[(dataset['MonthlyIncome_zscore'] > 2) | (dataset['MonthlyIncome_zscore'] < -2)]
```


```python
condition.shape
```




    (704, 13)




```python
dataset.drop(condition.index, inplace= True)
```


```python
dataset.shape
```




    (148642, 13)




```python
dataset.MonthlyIncome.plot.box()
```




    <AxesSubplot:>




    
![image]({{site.url}}/assets/project/output_68_1.png)
    



```python
dataset.MonthlyIncome.describe()
```




    count    148642.000000
    mean       6089.029790
    std        3775.044698
    min           0.000000
    25%        3900.000000
    50%        5400.000000
    75%        7333.000000
    max       32250.000000
    Name: MonthlyIncome, dtype: float64




```python
## If we want bin size of 1000 ,
bins = int((dataset.MonthlyIncome.max() - dataset.MonthlyIncome.min()) / 1000)
print(bins)
```

    32
    


```python
dataset.MonthlyIncome.plot.hist(bins=bins)
```




    <AxesSubplot:ylabel='Frequency'>




    
![image]({{site.url}}/assets/project/output_71_1.png)
    


There are 3 columns giving us information about Late Payments, lets look into them , one at a time.


```python
dataset["NumberOfTimes90DaysLate"].value_counts().sort_index()
```




    0     140389
    1       5211
    2       1551
    3        663
    4        291
    5        130
    6         80
    7         38
    8         21
    9         19
    10         8
    11         5
    12         2
    13         4
    14         2
    15         2
    17         1
    96         5
    98       220
    Name: NumberOfTimes90DaysLate, dtype: int64




```python
plt.xscale('log') ## this is to visualize better if not in log scale it is heavily skewed 
dataset["NumberOfTimes90DaysLate"].value_counts().sort_index().plot(kind= 'barh')
```




    <AxesSubplot:>




    
![image]({{site.url}}/assets/project/output_74_1.png)
    



```python
dataset["NumberOfTime60-89DaysPastDueNotWorse"].value_counts().sort_index()
```




    0     141111
    1       5706
    2       1116
    3        317
    4        104
    5         34
    6         16
    7          9
    8          2
    9          1
    11         1
    96         5
    98       220
    Name: NumberOfTime60-89DaysPastDueNotWorse, dtype: int64




```python
dataset["NumberOfTime30-59DaysPastDueNotWorse"].value_counts().sort_index()
```




    0     124823
    1      15953
    2       4574
    3       1744
    4        745
    5        341
    6        138
    7         54
    8         25
    9         12
    10         4
    11         1
    12         2
    13         1
    96         5
    98       220
    Name: NumberOfTime30-59DaysPastDueNotWorse, dtype: int64




```python
dataset["NumberOfDependents"].describe()
```




    count    144827.000000
    mean          0.757338
    std           1.114128
    min           0.000000
    25%           0.000000
    50%           0.000000
    75%           1.000000
    max          20.000000
    Name: NumberOfDependents, dtype: float64




```python
dataset["NumberOfDependents"].isnull().sum()
```




    3815




```python
dataset["NumberOfDependents"].plot.box()
```




    <AxesSubplot:>




    
![image]({{site.url}}/assets/project/output_79_1.png)
    



```python
dataset['NumberOfDependents'].median()
```




    0.0




```python
# IMPUTE
dataset['NumberOfDependents'].fillna(dataset['NumberOfDependents'].median(),inplace=True)
dataset["NumberOfDependents"].isnull().sum()
```




    0



### BI-VARIATE ANALYSIS - TWO VARIABLES AT A TIME

#### SeriousDlqin2yrs Vs. RevolvingUtilizationOfUnsecuredLines


```python
dataset['RevolvingUtilizationOfUnsecuredLines'].groupby(dataset.SeriousDlqin2yrs).mean().plot(kind='bar', color=['blue', 'green']) 
plt.ylabel('Ratio')
plt.title('Distribution of RevolvingUtilizationOfUnsecuredLines with label')
```




    Text(0.5, 1.0, 'Distribution of RevolvingUtilizationOfUnsecuredLines with label')




    
![image]({{site.url}}/assets/project/output_84_1.png)
    


Observation: Delinquent customers got almost twice the utilization of unsecured lines

#### SeriousDlqin2yrs Vs. Age


```python
dataset['age'].groupby(dataset.SeriousDlqin2yrs).mean().plot(kind='bar', color=['blue', 'green']) 
plt.ylabel('Age')
plt.title('Distribution of Age with label')
```




    Text(0.5, 1.0, 'Distribution of Age with label')




    
![image]({{site.url}}/assets/project/output_87_1.png)
    


Observation: On average lower aged customers are more delinquent 

#### SeriousDlqin2yrs Vs. DebtRatio


```python
dataset['DebtRatio'].groupby(dataset.SeriousDlqin2yrs).mean().plot(kind='bar', color=['blue', 'green']) 
plt.ylabel('DebtRatio')
plt.title('Distribution of Debt Ratio with label')
```




    Text(0.5, 1.0, 'Distribution of Debt Ratio with label')




    
![image]({{site.url}}/assets/project/output_90_1.png)
    


Observation: ??? Ask to Class

#### SeriousDlqin2yrs Vs. MonthlyIncome


```python
dataset['MonthlyIncome'].groupby(dataset.SeriousDlqin2yrs).mean().plot(kind='bar', color=['blue', 'green']) 
plt.ylabel('Monthly Income')
plt.title('Distribution of Monthly Income with label')
```




    Text(0.5, 1.0, 'Distribution of Monthly Income with label')




    
![image]({{site.url}}/assets/project/output_93_1.png)
    


Observation: ??? Ask to Class

### MULTI VARIATE ANALYSIS - more than two variables at a time, we will do correlation heatmap for this.


```python
## First lets drop the z_score columns we create to remove outliers
dataset=dataset.drop(['age_zscore', 'MonthlyIncome_zscore'], axis=1)

```


```python
dataset.columns
```




    Index(['SeriousDlqin2yrs', 'RevolvingUtilizationOfUnsecuredLines', 'age',
           'NumberOfTime30-59DaysPastDueNotWorse', 'DebtRatio', 'MonthlyIncome',
           'NumberOfOpenCreditLinesAndLoans', 'NumberOfTimes90DaysLate',
           'NumberRealEstateLoansOrLines', 'NumberOfTime60-89DaysPastDueNotWorse',
           'NumberOfDependents'],
          dtype='object')




```python
corr = dataset.corr()
#sns.heatmap(corr) # simple but shows more noisy plot, adding mask to only see half is better
mask = np.zeros_like(corr)
mask[np.triu_indices_from(mask)] = True
with sns.axes_style("white"):
    f, ax = plt.subplots(figsize=(10, 8))
    ax = sns.heatmap(corr, mask=mask, square=True)
```


    
![image]({{site.url}}/assets/project/output_98_0.png)
    


above figure shows that age and SeriousDlqin2yrs are highly correlated similarly NumberOfTimes90DaysLate and NumberOfTime30-59DaysPastDueNotWorse are less correlated. In the same way we can estimate the relationship between different attributes.

#### FEATURE ENGINEERING

What are some of the additional features we can create or drive from given attributes?
1. We have monthly income and total dependents, we can derive income per person
2. We have Debt to Income ratio so we can get total debt
3. From 1 & 2, we can get monthly balance
4. We can also sum all the dues , 30- 59 days, 60- 89 days, and 90 days

Let's add these 4 new features for now.


```python
# Income per person
dataset['Income_per_person'] = dataset['MonthlyIncome']/(dataset['NumberOfDependents']+1)
# Monthly Debt
dataset['Monthly_debt'] = dataset['DebtRatio']*dataset['MonthlyIncome']
# Monthly Balance
dataset['Monthly_balance'] = dataset['MonthlyIncome'] - dataset['Monthly_debt']
# Total number of DUEs
dataset['Total_number_of_dues'] = dataset['NumberOfTime30-59DaysPastDueNotWorse']+dataset['NumberOfTime60-89DaysPastDueNotWorse']+dataset['NumberOfTimes90DaysLate']

```


```python
dataset.head()
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
      <th>SeriousDlqin2yrs</th>
      <th>RevolvingUtilizationOfUnsecuredLines</th>
      <th>age</th>
      <th>NumberOfTime30-59DaysPastDueNotWorse</th>
      <th>DebtRatio</th>
      <th>MonthlyIncome</th>
      <th>NumberOfOpenCreditLinesAndLoans</th>
      <th>NumberOfTimes90DaysLate</th>
      <th>NumberRealEstateLoansOrLines</th>
      <th>NumberOfTime60-89DaysPastDueNotWorse</th>
      <th>NumberOfDependents</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0.766127</td>
      <td>45</td>
      <td>2</td>
      <td>0.802982</td>
      <td>9120.0</td>
      <td>13</td>
      <td>0</td>
      <td>6</td>
      <td>0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>0.957151</td>
      <td>40</td>
      <td>0</td>
      <td>0.121876</td>
      <td>2600.0</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>0.658180</td>
      <td>38</td>
      <td>1</td>
      <td>0.085113</td>
      <td>3042.0</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0.233810</td>
      <td>30</td>
      <td>0</td>
      <td>0.036050</td>
      <td>3300.0</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0</td>
      <td>0.213179</td>
      <td>74</td>
      <td>0</td>
      <td>0.375607</td>
      <td>3500.0</td>
      <td>3</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>



### MODEL BUILDING

Before we start modeling, we need to make sure what evaluation metrics to use. Since we have imbalanced data set, we will be using Precision- Recall, and f1-score for evaluation.

Class 1: (YES) : Delinquent Customers
Class 2: (NO): Non- Delinquent Customers

Here Class of Interest is positive class- which is Class 1. Lets discuss what could be more costly for business- whether False Positives or False Negatives.

If we predict customers will delinquent, but they are not. This means False Positives, because we falsely predicted positive class.

If we predict customers will NOT delinquent, but in reality they did. This means False Negatives, because we falsely predicted negative class.

From bank's perspective, False Negative is more costly, because we miss to predict the customers who will delinquent. Since False Negatives matter more, we should aim to reduce FNs, that means RECALL will be more important that PRECISION.

Precision = TP / TP + FP

Recall = TP / TP + FN



#### Steps to follow:
1. Split the data into train and test set (lets take 70-30 split)
2. Scale the data ( also called normalize): we can pick StandardScaler or MinMaxScaler
3. Try 3 different models: Logistic Regression, RandomForest, XGBoost
4. Compare the evaluation metrics
5. Pick the best performing and generalized model


```python
## TRAIN AND TEST SPLIT 70 to 30 percent

X = dataset.drop(columns=['SeriousDlqin2yrs'])
y = dataset['SeriousDlqin2yrs']
X_train, X_test, y_train, y_test = train_test_split(X, y,stratify= y,random_state=42,shuffle=True,test_size=0.3)
print('Shape of training data', X_train.shape)
print('-'*40)
print('Shape of test data', X_test.shape)
print('-'*40)

```

    Shape of training data (104049, 10)
    ----------------------------------------
    Shape of test data (44593, 10)
    ----------------------------------------
    


```python
## SCALE THE DATA, we will use standard scaler
sc= StandardScaler()
X_train_scaled=sc.fit_transform(X_train)
X_train_scaled=pd.DataFrame(X_train_scaled, columns=X.columns)

# Transform on test data
X_test_scaled=sc.transform(X_test)
X_test_scaled=pd.DataFrame(X_test_scaled, columns=X.columns)
```


```python
X_train_scaled.head()
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
      <th>RevolvingUtilizationOfUnsecuredLines</th>
      <th>age</th>
      <th>NumberOfTime30-59DaysPastDueNotWorse</th>
      <th>DebtRatio</th>
      <th>MonthlyIncome</th>
      <th>NumberOfOpenCreditLinesAndLoans</th>
      <th>NumberOfTimes90DaysLate</th>
      <th>NumberRealEstateLoansOrLines</th>
      <th>NumberOfTime60-89DaysPastDueNotWorse</th>
      <th>NumberOfDependents</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.027215</td>
      <td>1.475614</td>
      <td>-0.102208</td>
      <td>-1.283644</td>
      <td>0.112021</td>
      <td>-0.289289</td>
      <td>-0.062012</td>
      <td>-0.912388</td>
      <td>-0.055610</td>
      <td>0.239036</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.027219</td>
      <td>0.386825</td>
      <td>-0.102208</td>
      <td>-1.137202</td>
      <td>-0.183511</td>
      <td>0.099620</td>
      <td>-0.062012</td>
      <td>-0.912388</td>
      <td>-0.055610</td>
      <td>-0.666237</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-0.023049</td>
      <td>-0.429767</td>
      <td>-0.102208</td>
      <td>-0.397614</td>
      <td>0.367459</td>
      <td>-0.094834</td>
      <td>0.201595</td>
      <td>-0.015583</td>
      <td>0.209069</td>
      <td>1.144309</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.024338</td>
      <td>0.727071</td>
      <td>0.159529</td>
      <td>1.496206</td>
      <td>-0.183511</td>
      <td>0.294075</td>
      <td>-0.062012</td>
      <td>-0.015583</td>
      <td>-0.055610</td>
      <td>-0.666237</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-0.025999</td>
      <td>1.067318</td>
      <td>-0.102208</td>
      <td>0.137173</td>
      <td>-0.285739</td>
      <td>-0.483743</td>
      <td>-0.062012</td>
      <td>0.881221</td>
      <td>-0.055610</td>
      <td>-0.666237</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Creating metric function 
# Metrics to evaluate the model
def metrics_score(actual, predicted):
    print(classification_report(actual, predicted))
    cm = confusion_matrix(actual, predicted)
    plt.figure(figsize=(8,5))
    
    sns.heatmap(cm, annot=True,  fmt='.2f', xticklabels=['Not Delinquent', 'Delinquent'], yticklabels=['Not Delinquent', 'Delinquent'])
    plt.ylabel('Actual')
    plt.xlabel('Predicted')
    plt.show()
```


```python
X_train_scaled.isnull().sum()
```




    RevolvingUtilizationOfUnsecuredLines    0
    age                                     0
    NumberOfTime30-59DaysPastDueNotWorse    0
    DebtRatio                               0
    MonthlyIncome                           0
    NumberOfOpenCreditLinesAndLoans         0
    NumberOfTimes90DaysLate                 0
    NumberRealEstateLoansOrLines            0
    NumberOfTime60-89DaysPastDueNotWorse    0
    NumberOfDependents                      0
    dtype: int64




```python
# Fitting logistic regression model
lg=LogisticRegression(random_state=42, class_weight='balanced')
lg.fit(X_train_scaled,y_train)
```




    LogisticRegression(class_weight='balanced', random_state=42)




```python
# Checking the performance on the training data
y_pred_train = lg.predict(X_train_scaled)
metrics_score(y_train, y_pred_train)
```

                  precision    recall  f1-score   support
    
               0       0.97      0.79      0.87     97071
               1       0.19      0.66      0.29      6978
    
        accuracy                           0.78    104049
       macro avg       0.58      0.72      0.58    104049
    weighted avg       0.92      0.78      0.83    104049
    
    


    
![image]({{site.url}}/assets/project/output_111_1.png)
    



```python
# Checking the performance on the test dataset
y_pred_test = lg.predict(X_test_scaled)
metrics_score(y_test, y_pred_test)
```

                  precision    recall  f1-score   support
    
               0       0.97      0.78      0.86     41603
               1       0.19      0.72      0.30      2990
    
        accuracy                           0.77     44593
       macro avg       0.58      0.75      0.58     44593
    weighted avg       0.92      0.77      0.83     44593
    
    


    
![image]({{site.url}}/assets/project/output_112_1.png)
    



```python
# Printing the coefficients of logistic regression
cols=X.columns
coef_lg=lg.coef_
pd.DataFrame(coef_lg,columns=cols).T.sort_values(by = 0,ascending = False)
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
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>NumberOfTimes90DaysLate</th>
      <td>2.297865</td>
    </tr>
    <tr>
      <th>NumberOfTime30-59DaysPastDueNotWorse</th>
      <td>2.134538</td>
    </tr>
    <tr>
      <th>NumberOfTime60-89DaysPastDueNotWorse</th>
      <td>0.543397</td>
    </tr>
    <tr>
      <th>NumberOfDependents</th>
      <td>0.097003</td>
    </tr>
    <tr>
      <th>DebtRatio</th>
      <td>0.094698</td>
    </tr>
    <tr>
      <th>NumberRealEstateLoansOrLines</th>
      <td>0.062493</td>
    </tr>
    <tr>
      <th>NumberOfOpenCreditLinesAndLoans</th>
      <td>0.011010</td>
    </tr>
    <tr>
      <th>RevolvingUtilizationOfUnsecuredLines</th>
      <td>-0.012984</td>
    </tr>
    <tr>
      <th>MonthlyIncome</th>
      <td>-0.147554</td>
    </tr>
    <tr>
      <th>age</th>
      <td>-0.450574</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Predict_proba gives the probability of each observation belonging to each class
y_scores_lg=lg.predict_proba(X_train_scaled)
precisions_lg, recalls_lg, thresholds_lg = precision_recall_curve(y_train, y_scores_lg[:,1])

# Plot values of precisions, recalls, and thresholds
plt.figure(figsize=(10,7))
plt.plot(thresholds_lg, precisions_lg[:-1], 'b--', label='precision')
plt.plot(thresholds_lg, recalls_lg[:-1], 'g--', label = 'recall')
plt.xlabel('Threshold')
plt.legend(loc='upper left')
plt.ylim([0,1])
plt.show()
```


    
![image]({{site.url}}/assets/project/output_114_0.png)
    



```python
## Intersection of Precision and Recall is Optimum threshold
optimal_threshold=.78
y_pred_train = lg.predict_proba(X_train_scaled)

metrics_score(y_train, y_pred_train[:,1]>optimal_threshold)
```

                  precision    recall  f1-score   support
    
               0       0.95      0.98      0.96     97071
               1       0.49      0.25      0.33      6978
    
        accuracy                           0.93    104049
       macro avg       0.72      0.62      0.65    104049
    weighted avg       0.92      0.93      0.92    104049
    
    


    
![image]({{site.url}}/assets/project/output_115_1.png)
    



```python
optimal_threshold=.78
y_pred_test = lg.predict_proba(X_test_scaled)
metrics_score(y_test, y_pred_test[:,1]>optimal_threshold)
```

                  precision    recall  f1-score   support
    
               0       0.95      0.97      0.96     41603
               1       0.42      0.33      0.37      2990
    
        accuracy                           0.92     44593
       macro avg       0.69      0.65      0.66     44593
    weighted avg       0.92      0.92      0.92     44593
    
    


    
![image]({{site.url}}/assets/project/output_116_1.png)
    


**Observation:**
- The model is giving **similar performance on the test and train data** i.e. the model is giving a generalized performance.
- **The precision of the test data has increased significantly** while at the same time, the recall has decreased, which is to be expected while adjusting the threshold.
- Since RECALL is important for us as discussed abaove before we began model building, we CANNOT use higher threshold to lose the recall.
- The average recall and precision for the model are good but let's see if we can get better performance using other algorithms. 

**Remember our goal is to have better Recall**


```python
# Fitting the Random Forest classifier on the training data
rf_estimator = RandomForestClassifier(class_weight = {0: 0.93, 1: 0.07}, random_state = 42) ## class weight comes from initial class distribution
rf_estimator.fit(X_train_scaled, y_train)
```




    RandomForestClassifier(class_weight={0: 0.93, 1: 0.07}, random_state=42)




```python
# Checking performance on the training data
y_pred_train_rf = rf_estimator.predict(X_train)
metrics_score(y_train, y_pred_train_rf)
```

                  precision    recall  f1-score   support
    
               0       0.97      0.65      0.78     97071
               1       0.13      0.72      0.22      6978
    
        accuracy                           0.66    104049
       macro avg       0.55      0.68      0.50    104049
    weighted avg       0.91      0.66      0.74    104049
    
    


    
![image]({{site.url}}/assets/project/output_119_1.png)
    



```python
# Checking performance on the testing data
y_pred_test_rf = rf_estimator.predict(X_test)
metrics_score(y_test, y_pred_test_rf)
```

                  precision    recall  f1-score   support
    
               0       0.97      0.65      0.78     41603
               1       0.13      0.72      0.22      2990
    
        accuracy                           0.65     44593
       macro avg       0.55      0.69      0.50     44593
    weighted avg       0.91      0.65      0.74     44593
    
    


    
![image]({{site.url}}/assets/project/output_120_1.png)
    


<font color= red> You can uncomment and run below cell once to find the best model using GridSearch. I added the code to save the model into the physical drive after finding the best model. So it can be commented again to save the runtime. 


```python
## RF with GRIDSEARCH- It will be computationally costly but we shall get better model
# For tuning the model-- Dont run again
# from sklearn.model_selection import StratifiedKFold
# from sklearn.model_selection import GridSearchCV

# skf = StratifiedKFold(n_splits=5, shuffle=True, random_state=5)

# rf = RandomForestClassifier(n_estimators=100, n_jobs=-1, random_state=42, 
#                             class_weight='balanced')
# parameters = {'max_features': [1, 2, 4], 'min_samples_leaf': [3, 5, 7, 9], 'max_depth': [5,10,15]}
# rf_grid_search = GridSearchCV(rf, parameters, n_jobs=-1, scoring='roc_auc', cv=skf, verbose=True)
# rf_grid_search = rf_grid_search.fit(X_train, y_train)

# ## SAVING MODEL AS PICKLE FILE, SO you can simply load it in future
# model_save_name = '/content/drive/MyDrive/givemecredit_bestmodel.pkl'
# joblib.dump(rf_grid_search.best_estimator_, model_save_name)

```


```python
## load the pre-trained model from physical drive
model_save_name = '/content/drive/MyDrive/givemecredit_bestmodel.pkl'
loaded_model = joblib.load(model_save_name)
# Checking performance on the testing data
y_pred_test= loaded_model.predict(X_test)
metrics_score(y_test, y_pred_test)
```

                  precision    recall  f1-score   support
    
               0       0.98      0.84      0.90     41603
               1       0.24      0.71      0.36      2990
    
        accuracy                           0.83     44593
       macro avg       0.61      0.77      0.63     44593
    weighted avg       0.93      0.83      0.86     44593
    
    


    
![image]({{site.url}}/assets/project/output_123_1.png)
    



```python
importances = loaded_model.feature_importances_
columns = X.columns
importance_df = pd.DataFrame(importances, index = columns, columns = ['Importance']).sort_values(by = 'Importance', ascending = False)
plt.figure(figsize = (13, 13))
sns.barplot(importance_df.Importance, importance_df.index);
```


    
![image]({{site.url}}/assets/project/output_124_0.png)
    


### Conclusion:
With Grid Search and 5 fold Cross Validation, we were able to find best model with Training Accuracy of 84% and Test Accuracy of 83% , since both training and test accuracy are similar, our model is generalized. We were also able to maintain the Recall for positive class (Delinquent Customers) around 71%. So compared to all the models we tried, this is the best one to pick.

#### More things you can try:
1. Trying more models: SVMs, and Boosting Models could be other options to try
2. Balancing the class- with some sampling techniques and try again
3. Additional Feature Engineering


```python

```
