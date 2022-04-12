---
title:  "Machine Learning: Linear Regression with Different Gradient Decent Algorithms"
date:   2022-04-02 09:29:17 +0545
categories: Machine Learning
tags:
  
  - Python
  - Regression Model
header:
  teaser: "assets/gradient/output_14_0.png"
  overlay_image: "assets/gradient/output_14_0.png"
toc: true
---
# Mini- Batch Gradient Decent

## Import necessary module
* `pandas` : Working for DataFrame
* `numpy` : For array operation 
* `matplotlib` : for visualization

Read csv data in pandas Dataframe



```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
df = pd.read_csv('F:/MDS-Private-Study-Materials/Second Semester/Applied Machine Learning/data.csv')
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
      <th>x</th>
      <th>y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>32.502345</td>
      <td>31.707006</td>
    </tr>
    <tr>
      <th>1</th>
      <td>53.426804</td>
      <td>68.777596</td>
    </tr>
    <tr>
      <th>2</th>
      <td>61.530358</td>
      <td>62.562382</td>
    </tr>
    <tr>
      <th>3</th>
      <td>47.475640</td>
      <td>71.546632</td>
    </tr>
    <tr>
      <th>4</th>
      <td>59.813208</td>
      <td>87.230925</td>
    </tr>
  </tbody>
</table>
</div>



## Split Data
 We split data into train set and test set in the ratio of 70% to 30%


```python
split = int(len(df)*0.7)
train_x, test_x = df[:split].x , df[split:].x
train_y, test_y = df[:split].y , df[split:].y

len(test_x)
```




    30



## Create class `Mini_batch_gradient_decent`

Create method `create_batch` inside class which takes train data, test data and batch_sizes as parameter. We create `mini_batches = []` to store the value of each batches. `data = np.stack((train_x,train_y), axis=1)` function join train_x and train_y into first dimension.

 Number of batches is row divide by batches size. We use for loop in the range of no_of_batches. ` mini_batch = data[i * batch_size: (i+1)* batch_size]` which create mini batch from 0 to if we give batch_size 10 upto 10 in the next iteration mini_batch will be 10 to 20 and so on. If number of row is not exactly divided by batch size then there will be data remain outside of batch so we will do `train_x.shape[0]%batch_size != 0` then we will keep all the batch data into mini_batches list by using append function. In first column we kept x values and in second column we kept y values. Finally we return mini_batches.



```python
class Mini_batch_gradient_decent:

    
    
    def create_batch(self,train_x, train_y, batch_size):
        mini_batches = []
        data = np.stack((train_x,train_y), axis=1)

        no_of_bathches = train_x.shape[0]//batch_size
        
        for i in range(no_of_bathches):
            
            mini_batch = data[i * batch_size: (i+1)* batch_size]
           
            mini_batches.append((mini_batch[:,0],mini_batch[:,1]))
        if train_x.shape[0]%batch_size != 0:
            mini_batchi = data[i* batch_size:]
            mini_batches.append((mini_batch[:,0],mini_batch[:,1]))
        return mini_batches
```

# Model Fitting

The function `fit()` is defined, with the parameters `train x, train y, alpha, epochs, batch size`. Then we set the slope and intercept values to 1 and 1, respectively. In addition, the letter l denotes the total number of observations. In the range of epochs, we used for loop. The batch function is then called, as explained in the previous cell block. We utilize the for loop in batches again, this time with xb indicating batch x values and yb indicating batch y values, and then we reshape the xb and yb. We can take all rows but only one column with `xb.reshape(-1,1)`. The same is true for y. Define the linear regression projected value now. The mean square error is next defined, and finally, the mean square error is calculated.


```python
import time 
class Mini_batch_gradient_decent:

    
    
    def create_batch(self,train_x, train_y, batch_size):
        mini_batches = []
        data = np.stack((train_x,train_y), axis=1)

        no_of_bathches = train_x.shape[0]//batch_size
        
        for i in range(no_of_bathches):
            
            mini_batch = data[i * batch_size: (i+1)* batch_size]
           
            mini_batches.append((mini_batch[:,0],mini_batch[:,1]))
        if train_x.shape[0]%batch_size != 0:
            mini_batchi = data[i* batch_size:]
            mini_batches.append((mini_batch[:,0],mini_batch[:,1]))
        return mini_batches   
    
    def fit(self, train_x, train_y, alpha, epochs, batch_size):
        
        
        self.m = np.random.randn(1,1)
        self.c = np.random.randn(1,1)
        
        l = len(train_x)
        
        for i in range(epochs):

            batches = self.create_batch(train_x, train_y, batch_size)
            
            t1=time.time()
            for batch in batches:
                
                xb = batch[0]
                yb = batch[1]
                n = len(xb)
                
                xb = xb.reshape(-1,1)
                #print(xb)
                yb = yb.reshape(-1,1)
                #print(yb)
                
                delta_intercept = None
                delta_slope = None
                yp = np.dot(xb, self.m)+self.c
                
                
                err=(0.5/n) * np.sum((yb-yp)**2)
                
                delta_intercept = -(1/n) * np.sum(yb-yp)
                delta_slope = -(1/n) * np.sum((yb-yp)*xb)
                
#                 intercept = np.mean((np.dot(self.m,xb.T) + self.c)-yb)
#                 slope = np.mean(((np.dot(self.m,xb.T)+ self.c)-yb)*xb)

                self.m = self.m - alpha* (delta_slope)
                self.c = self.c - alpha * (delta_intercept)
            #print(f"Iteration {i}: Error: {err}, time = {(time.time()-t1)/60}")
            
            
    def slope_intercept(self):
        print(f"Slope is {self.m[0][0]}")
        print(f"Intercept is {self.c[0][0]}")
    
    def predict(self, test_x):
        test_x = test_x.reshape(test_x.shape[0],1)
        self.m = self.m.reshape((self.m.shape[0],self.m.shape[0]))
        result = np.dot(test_x,self.m) + self.m
        return result
                                
                
        
```

##  Function for slope, intercept and prediction
 
 We define code blocks for slope and intercept as well as prediction in the code block below. The prediction function takes the value of test x and returns the result.


```python

    def slope_intercept(self):
        print(f"Slope is {self.m[0][0]}")
        print(f"Intercept is {self.c[0][0]}")
    
    def predict(self, test_x):
        test_x = test_x.reshape(test_x.shape[0],1)
        self.m = self.m.reshape((self.m.shape[0],self.m.shape[0]))
        result = np.dot(test_x,self.m) + self.m
        return result
                                
                
        
```

##  Function call
We use our own dummy data to invoke the function here. The goal of using this data is to determine whether or not our model is functioning appropriately. Our model is looking fantastic. Our model should give us a value for c 1 and a value for m 1500, and we can see that it does.




```python
mgd = Mini_batch_gradient_decent()


mgd.fit(np.arange(1,500)/500, 1+3*np.arange(1,500),0.01,5000, 32)
```


```python
mgd.slope_intercept()
```

    Slope is 1499.999999999971
    Intercept is 1.0000000000151974
    


```python
mgd.fit(train_x, train_y,0.0001,5000, 16)
```


```python
plt.scatter(train_x, train_y)
plt.plot(train_x, np.dot(train_x.to_numpy().reshape(-1,1), mgd.m)+mgd.c, c="r")
plt.show()
```


    
![]({{site.url}}/assets/gradient/output_14_0.png)
    


# Batch gradient decent
The function `define gradient decent()` takes the parameters `train x, y true, epochs, learning rate`. Set the value of m and c to 1. Make an empty list to keep track of the number of errors in each iteration. The entire length of observations is denoted by the letter l. Use for loops in the period range. Define xb and yb from train x and y true, respectively, where `.reshape(-1,1)` indicates that we can choose any rows but only one column. Define yp now. Then define what square mistake implies. Then, for both slope and intercept, determine the gradient. After that, change the values of the parameters m and c. Finally, we provided dummy data before testing our model on real data to ensure that it was working properly.


```python
def batch_gradient_decent(train_x, y_true, epochs, learning_rate = 0.001):
    
    m = np.random.randn(1,1)
    c = np.random.randn(1,1)
    l = len(train_x)
    errs = []
    
    for i in range(epochs):
        t1= time.time()
        
        xb = train_x.reshape(-1,1)
        yb = y_true.reshape(-1,1)
        
        delta_intercept = None
        delta_slope = None
        yp = np.dot(xb, m)+c

        n = len(xb)
        err=(0.5/n) * np.sum((yb-yp)**2)

        delta_intercept = -(1/n) * np.sum(yb-yp)
        delta_slope = -(1/n) * np.sum((yb-yp)*xb)
        
        #print(f"Iteration {i}: Error: {err}, time: {(time.time()-t1)/60}")
        m = m - learning_rate * delta_slope
        c = c- learning_rate* delta_intercept
        errs.append(err)
    return m, c, errs
        

    

m,c,errs=batch_gradient_decent(np.arange(1,500)/500, 1+3*np.arange(1,500),5000,0.1)
```

In our case error is decreasing rapidly in some iterations and decreasing gradually in last some iterations.


```python
plt.plot(errs)
```




    [<matplotlib.lines.Line2D at 0x25bc8914b20>]




    
![]({{site.url}}/assets/gradient/output_18_1.png)
    



```python
batch_gradient_decent(train_x.to_numpy(), train_y.to_numpy(),5000,0.0001)
```




    (array([[1.47579742]]),
     array([[-0.85511292]]),
     [213.99911978766565,
      146.87032454589203,
      108.8473323531241,
      87.3104049141196,
      75.11148923200925,
      68.2017959855974,
      64.2880160773431,
      62.071176851560864,
      60.81551618964752,
      60.10428482994466,
      59.70142828867082,
      59.473240943669325,
      59.34398945952593,
      59.27077707542778,
      ...])



# Stochastic Gradient Decent
if we keep value of `batch_size = 1` in mini-batch gradient decent then it becomes stochastic gradient decent.




```python
class Stochastic_gradient_decent:

    
    
    def create_batch(self,train_x, train_y, batch_size):
        mini_batches = []
        data = np.stack((train_x,train_y), axis=1)

        no_of_bathches = train_x.shape[0]//batch_size
        
        for i in range(no_of_bathches):
            
            mini_batch = data[i * batch_size: (i+1)* batch_size]
           
            mini_batches.append((mini_batch[:,0],mini_batch[:,1]))
        if train_x.shape[0]%batch_size != 0:
            mini_batchi = data[i* batch_size:]
            mini_batches.append((mini_batch[:,0],mini_batch[:,1]))
        return mini_batches

    def fit(self, train_x, train_y, alpha, epochs, batch_size):


        self.m = np.random.randn(1,1)
        self.c = np.random.randn(1,1)

        l = len(train_x)

        for i in range(epochs):

            batches = self.create_batch(train_x, train_y, batch_size)

            t1=time.time()
            for batch in batches:

                xb = batch[0]
                yb = batch[1]
                n = len(xb)

                xb = xb.reshape(-1,1)
                #print(xb)
                yb = yb.reshape(-1,1)
                #print(yb)

                delta_intercept = None
                delta_slope = None
                yp = np.dot(xb, self.m)+self.c


                err=(0.5/n) * np.sum((yb-yp)**2)

                delta_intercept = -(1/n) * np.sum(yb-yp)
                delta_slope = -(1/n) * np.sum((yb-yp)*xb)

    

                self.m = self.m - alpha* (delta_slope)
                self.c = self.c - alpha * (delta_intercept)
            #print(f"Iteration {i}: Error: {err}, time = {(time.time()-t1)/60}") 

            
    def slope_intercept(self):
        print(f"Slope is {self.m[0][0]}")
        print(f"Intercept is {self.c[0][0]}")
    
    def predict(self, test_x):
        test_x = test_x.reshape(test_x.shape[0],1)
        self.m = self.m.reshape((self.m.shape[0],self.m.shape[0]))
        result = np.dot(test_x,self.m) + self.m
        return result
                                
                
        
```


```python
mgd = Stochastic_gradient_decent()


mgd.fit(np.arange(1,500)/500, 1+3*np.arange(1,500),0.01,5000, 1)
```

# Comparison  Between Three Gradient decent in terms of time

Batch-gradient decent and mini-batch-gradient decent are fast as compare to stochastic gradient decent.


```python

```
