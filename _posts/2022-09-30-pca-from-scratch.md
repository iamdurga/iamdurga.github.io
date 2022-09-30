---
title:  "PCA from scratch"
date:   2022-09-30 09:29:17 +0545
categories: Machine Learning
tags:
  - Unsupervised Learning
  - clustering
  - Dimensionality Reduction
header:
  teaser: "assets/monte/output_5_0.png"
  overlay_image: "assets/monte/output_5_0.png"
toc: true
---
# Introduction 
A method of dimensional reduction is PCA. When a machine learning method has a large number of features, we must choose the features that contribute the most and ignore the datasets that are less significant. This is where PCA comes into play. Consequently, PCA is an unsupervised method for choosing useful datasets from a huge collection of features. It is a statistical technique that converts the observations of correlated features into a set of linearly uncorrelated features via an orthogonal transformation.

## PCA on Numerical Dataset
**Given the following data use PCA to reduce the dimension from 2 to 1.**

|  Feature | EN.1  |  EN.2 | EN.3  | EN.4  |
|---|---|---|---|---|
|  x | 4  | 8  | 13  | 7  |
|  y | 11  | 4  |  5 | 14  |

Following are the steps to obtained the required number of PCA.

#### Step1: Dataset

|  Feature | EN.1  |  EN.2 | EN.3  | EN.4  |
|---|---|---|---|---|
|  x | 4  | 8  | 13  | 7  |
|  y | 11  | 4  |  5 | 14  |



No.of feature, n = 2

No.of Sample, N = 4

#### Step2: Computation of mean of variables

$$ \bar{x} = \frac{4 + 8 + 13 + 7}{4}= 8$$
$$ \bar{y} = \frac{11 + 4 + 5+ 14}{4}= 8.5$$

#### Step3: Computation of covariance matrix
ordered paired are,
(x, x), (x, y), (y, x), (y, y)

If we have n variables then we have $$n^2$$ ordered pair.

**(i) Covariance of all ordered pairs**

$$ cov(x,x) = \frac{1}{N-1} \sum_{k = 1}^{N}(xik - \bar{xi}) (xij - \bar{xj}) $$

$$ =\frac{1}{4-1}[(4- 8)^2 + (8- 8)^2 + (13- 8)^2 + (7- 8)^2]= 14 $$



$$ cov(x,y) = \frac{1}{4-1}[(4- 8)(11- 8.5) + (8- 8)(4- 8.5) + (13- 8)(5- 8.5) + (7- 8)(14- 8.5)] = -11 $$

$$cov(x,y) = cov(y, x) = -11$$

$$ cov(y, y) =  \frac{1}{4-1}[(11- 8.5)^2 + (4- 8.5)^2 + (5- 8.5)^2 + (14- 8.5)^2]= 23 $$

**(ii) Covariance Matrix**

|  cov(x,x) | cov(x,y)  | 
|---|---|
|  cov(y,x) | cov(y,y) | 
 
 
 |  14| -11  | 
|---|---|
|  -11 | 23| 

####  Step 4:Eigen value, Eigen vector, Normalized Eigen vector
 
 **(i) Eigen Values** 
 
 $$ det(S- \lambda I) = (14 - \lambda)(23 - \lambda) - (-11 \times -11) $$
 
 lambda = 30.38, 6.61
 
 **(ii) Eigen Vectors** 
 $$ (S- \lambda 1 I)U1 = 0 $$
 $$ (14- \lambda 1)U1 - 11 U2 = 0$$
$$ -11 U1 - (23- \lambda 1)U2 = 0$$

Hence,normalized eigen vector u1 of 𝜆1 i.e e1 [-0.83025082,  0.55738997]

for 𝜆2 normalized eigen vector i.e e2 [-0.55738997, -0.83025082]

**Step5: Derive New Dataset** 

|  Feature | EN.1  |  EN.2 | EN.3  | EN.4  |
|---|---|---|---|---|
|  pc1 | p11 | p12  | p13  | p14 |

**for pc1**:
$$ p11 = e1^T[-4, 2.5]^T = -4.008989537218968 $$
$$ p12 = e1^T[0, 3.5]^T = 3.7361286866113304$$
$$ p13 = e1^T[5, -2.5]^T = 0.1539328264398951$$
$$ p14 = e1^T[-1, 6]^T = 0.1189280241677419$$

|  Feature | EN.1  |  EN.2 | EN.3  | EN.4  |
|---|---|---|---|---|
|  pc1 | -4.008 | 3.736 | 0.153  | 0.118 |

	


# PCA Using Python

# Import Necessary Module


```python
import numpy as np
import pandas as pd
```

# DataSet


```python
#Understanding the mathematics behind PCA
A = np.matrix([[4,8,13,7],
               [11,4,5,14]])
```


```python
A.shape
```




    (2, 4)




```python
dataset = pd.DataFrame(A,columns  = ['EN1','EN2','EN3','EN4'], index = ["x","y"])
dataset
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
      <th>EN1</th>
      <th>EN2</th>
      <th>EN3</th>
      <th>EN4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>x</th>
      <td>4</td>
      <td>8</td>
      <td>13</td>
      <td>7</td>
    </tr>
    <tr>
      <th>y</th>
      <td>11</td>
      <td>4</td>
      <td>5</td>
      <td>14</td>
    </tr>
  </tbody>
</table>
</div>



# Compute the mean of variable


```python
np.mean(dataset,1)
```




    x    8.0
    y    8.5
    dtype: float64



# Compute covariance matrix


```python
cov_mat = dataset.T.cov()
cov_mat
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
      <th>x</th>
      <th>y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>x</th>
      <td>14.0</td>
      <td>-11.0</td>
    </tr>
    <tr>
      <th>y</th>
      <td>-11.0</td>
      <td>23.0</td>
    </tr>
  </tbody>
</table>
</div>




# Computation of eigenvalues and eigenvectors


```python
w, v = np.linalg.eig(cov_mat)
```


```python
w
```




    array([ 6.61513568, 30.38486432])




```python
v
```




    array([[-0.83025082,  0.55738997],
           [-0.55738997, -0.83025082]])




```python
v[1:].T
v[1:].shape
```




    (1, 2)



# Computation of first principal component


```python
p11 = np.dot(v[1:],  np.array([[4-8],[11-8.5]]))
p11

```




    array([[0.15393283]])




```python
p12 = np.dot(v[1:],  np.array([[8-8],[4-8.5]]))
p12

```




    array([[3.73612869]])




```python
p13 = np.dot(v[1:],  np.array([[13-8],[5-8.5]]))
p13

```




    array([[0.11892802]])




```python
p14 = np.dot(v[1:],  np.array([[7-8],[14-8.5]]))
p14

```




    array([[-4.00898954]])




```python
pc1 = [p11,p12,p13,p14]

```


```python
pd.Series(pc1)
```




    0    [[0.1539328264398951]]
    1    [[3.7361286866113304]]
    2    [[0.1189280241677419]]
    3    [[-4.008989537218968]]
    dtype: object




```python

```
