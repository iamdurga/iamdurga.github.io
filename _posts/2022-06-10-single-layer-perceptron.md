---
title:  "Single Layer Perceptron From Scratch"
date:   2022-06-10 09:29:17 +0545
categories: Machine Learing
tags:
  - Neural Network
  - Python
  
header:
  teaser: "assets/header_images/2.png"
  overlay_image: "assets/header_images/2.png"
toc: true
---
# Artificial Neuron Network

The term "neural network" refers to an artificial neural network (ANN) (NN), which is a computational paradigm inspired by the way the human brain or nervous system performs computation. Perception, pattern recognition, motor control, and other computations are all performed by the brain, which is a highly complex, non-linear, and parallel computational machine. The basic structural unit of the brain is the neuron or nerve cell. The basic structure of a neural network looks like the following, containing a number of input layers, hidden layers, and an output layer. The output produced depends on the activation function used.


Humans can complete work far faster than today's fastest digital machines, and this is made possible by the parallel computation of neurons that are linked together.

# Biological Neuron Network
The figure below shows the basic structure of a biological neuron network. A human neuron consists of a cell body for signal processing, many dendrites to receive signals, an axon for outputting the result, and synapses between the axon and dendrites of other cells.




## Modes of Neuron

Basically, models of neurons can be divided into two parts:

1. Deterministic model of Neuron
2. Stochastic model of Neuron

**Deterministic Model of Neuron** 

Three basic elements of this neural model are:

1. **Synapses** or connecting links: These are the connecting links used to link the inputs of the neuron network. Each link is characterized by a weight that defines the strength of the link.

2. **Adder**: The adder is responsible for finding the weighted sum of inputs to the neuron.

3. **Activation Function**: The activation function is responsible for determining the output of the neuron. It is also referred to as the squashing function.

**Stochastic model of Neuron** 

For all inputs, the deterministic neural model precisely describes input–output behavior. However, the stochastic neuron model causes non-deterministic input-output behavior. The activation function utilized in deterministic neural models is given a probabilistic interpretation in stochastic neural models.

In the stochastic neural model, a neuron is only allowed to be in one of two states: +1 (ON) or -1 (OFF). A neuron's decision to fire is probabilistic. Let x denote the neuron's state, and P(v) denote the probability of firing, where v is the neuron's activation potential.


$$ P(v) = \frac{1}{1 + e ^\frac{-v}{T}} $$ 

This makes the input-output behavior stochastic by adding uncertainty to neuron firing. Everything else in the stochastic neuron model remains the same as it is in the deterministic model.

## Modes of activation function



## Activation Function

The activation function, also known as the hard limiter function, is responsible for converting the input of an ANN into an output. The activation function performs a nonlinear transformation of the input signal. The output is then processed and serves as input to the next layer of neurons.

There are different types of activation functions, and some of them are listed below:

* Threshold

* Linear

* Sigmoid

* Tanh


## Structures of Neural Network

The structure of neurons in a neural network is referred to as neural network architecture. In general, there are three types of neural network topologies or structures:

1. **Single Layer Feedforward Neural Network**

2. **Multilayer Feedforward Neural Network**

3. **Recurrent Neural Network**

In this blog, I am going to describe how a single-layer neural network works and how to implement it from scratch.

## Single Layer Feed Forward Neuron Network

It's the most basic type of network architecture. In this architecture, we have an input layer of source nodes that is directly connected to an output layer of neurons (computation nodes), but not the other way around.

## Learning In Neuron Network

The ability of artificial neural networks to learn is one of their most striking capabilities. Artificial neural networks (ANNs) learn by altering the network's weighted connections between neurons. The following are the learning rules for neural networks:

* Hebbian Learning Rule

* Perceptron Learning Rule

* Backpropagation Learning etc.

## Hebbian Learning Rule

The rule is based on the idea that if two neighboring neurons activate and deactivate at the same time, their connection weights should increase. Conversely, the weight difference between neurons operating in opposite phases should decrease. If there is no signal connection, the weight should remain unchanged. This assumption can be described using the following formula.

$$ \delta(w_{ij}) = \alpha * x_i * y_i$$

>>where $w_{ij}$  is weight form neuron i to neuron j,
>>$\alpha$ is learning rate,
>>$x_i$ is input,
>>$y_i$ is output
  

## Hebbian Learing Algorithm

* Initialize all weights and bias to zero

* For each training vector s and target t perform steps 3 to 6
*  Set $ s_i = x_i $ for i = 1 to n
* Set y = t
* Adapt weight as $ w_i = w_i + \alpha * x_i *y$
* Adapt bias as $ b + \alpha * y$
* Test for stopping condition

## Hebbian Learing Algorithm from  scratch

Import module numpy which is used for mathematical calculations.


```python
import numpy as np
```

Initially, initialize the bias and learning rate to zero. Define the function `hebb_train()` to train the Hebbian learning algorithm. Now, run a for loop from 0 to the size of observations, where `dw` and `db` represent the updating factors for weight and bias, respectively.


```python
b=0
alpha=1

def hebb_train(x,y,w):
    for i in range(0,len(x)):
        global b
        dw=alpha*x[i]*y[i]
        db=alpha*y[i]
        w=np.add(w,dw)
        b=b+db
        print("After Interation ",i+1," :Weights")
        print(w)
        print("Bias:",b)    
    return w
```

The following block of code is for the activation function. In this example, we are using the threshold function as the activation function. If the values are greater than a certain threshold value, we assign class 1; otherwise, we set it to class 0.


```python
def hebb_predict(x,w):  
  z=x*w
  tx=sum(z)
  y=f(tx)
  return y
```

Following block of code is for activation function. Here in this example we are using threshold function as activation function. If values are grater than certain threshold value then we give class 1 else we set class 0.




```python
def f(x):
    if(x>b):
        return 1
    else:
        return 0
```

In the code shell below we build four observation having two columns and train y as only column vectors which is result of AND gate. We again take testx is same as trainx. Initially we initialize weight zero. Then we called respective function which we define previously as per our requirement


```python
trainx=np.array([[1,1],[1,0],[0,1],[0,0]])
trainy=np.array([1,0,0,0])
testx=np.array([[1,1],[1,0],[0,1],[0,0]])
wt=np.array([0,0])
print("+++++++++")
for i in range(1,5):
  print("Epoch#",i)
  wt=hebb_train(trainx,trainy,wt)
print("Final Weights:")
print(wt)
for x in testx:
  out=hebb_predict(x,wt)
  print("Input:",x)
  print("Output:",out)
```

    +++++++++
    Epoch# 1
    After Interation  1  :Weights
    [1 1]
    Bias: 1
    After Interation  2  :Weights
    [1 1]
    Bias: 1
    After Interation  3  :Weights
    [1 1]
    Bias: 1
    After Interation  4  :Weights
    [1 1]
    Bias: 1
    Epoch# 2
    After Interation  1  :Weights
    [2 2]
    Bias: 2
    After Interation  2  :Weights
    [2 2]
    Bias: 2
    After Interation  3  :Weights
    [2 2]
    Bias: 2
    After Interation  4  :Weights
    [2 2]
    Bias: 2
    Epoch# 3
    After Interation  1  :Weights
    [3 3]
    Bias: 3
    After Interation  2  :Weights
    [3 3]
    Bias: 3
    After Interation  3  :Weights
    [3 3]
    Bias: 3
    After Interation  4  :Weights
    [3 3]
    Bias: 3
    Epoch# 4
    After Interation  1  :Weights
    [4 4]
    Bias: 4
    After Interation  2  :Weights
    [4 4]
    Bias: 4
    After Interation  3  :Weights
    [4 4]
    Bias: 4
    After Interation  4  :Weights
    [4 4]
    Bias: 4
    Final Weights:
    [4 4]
    Input: [1 1]
    Output: 1
    Input: [1 0]
    Output: 0
    Input: [0 1]
    Output: 0
    Input: [0 0]
    Output: 0
    

## Single Layer FeedForward Using perceptron

The perceptron is the most basic type of neural network for identifying patterns that are linearly separable. Linearly separable patterns are those that can be divided by a hyperplane. Essentially, a perceptron consists of a single neuron with adjustable synaptic weights and bias.

The pattern classification capability of a perceptron, based on a single neuron, is limited to only two classes. Classification with more than two classes can be achieved by increasing the output layer of the perceptron to include more than one neuron. For the perceptron to perform properly, the classes must be linearly separable.
The hard limiter input of perceptron is,

$$ v = \sum(w_ix_i + b)$$



Because AND and OR functions are linearly separable, a perceptron can be trained to demonstrate behavior of both. However, because the XOR function is not linearly separable, perceptrons cannot be trained to learn its behavior.

Error correction rule for perceptron : $$ v = \sum w_i y_i $$

Now, we can write weight update rule for nth step as below,

**Case I** : For correct classification
$$ w^T(n) x(n) > 0$$ and $$ x(n) \in c_1$$ then $$ w(n+1) = w(n) $$

$$ w^T(n) x(n) <= 0$$ and $$ x(n) \in c_2$$ then $$ w(n+1) = w(n) $$

**Case II**: Misclassification 

$$ w^T(n) x(n) > 0$$ and $$ x(n) \in c_2$$ then $$ w(n+1) = w(n)-\alpha x(n) $$

$$ w^T(n) x(n) <= 0$$ and $$ x(n) \in c_1$$ then $$ w(n+1) = w(n)+\alpha x(n) $$

Thus, we can represent weight change rule using single equation as below
$$ w(n + 1) = w(n) + \alpha x(n)(t(n) - y(n)) $$ where y(n) is actual output and t(n) is target output.


## Perceptron Learing Algorithm

* Initialize all weights and bias to zero

* For each training vector s and target t perform steps 3 to 6

* Set $$x_i = s_i$$ for i = 1 to n

* Compute output using Hard limiter activation function as below,
$$ y_{in} = b + \sum_{n=1}^{10}(w_i x_i)$$

* Adapt weights as: $$ w_i = w_i + \alpha(t - y)x_i$$

* Adapt weights as: $$ b_i = b_i + \alpha(t-y) $$
* Test for stopping condition.


## Perceptron Learning from scratch


```python
import numpy as np
```


```python
b = 0
alpha = 1
def percept_train(x,y,w):
    for i in range(0,len(x)):
        global b
        yact = per_predict(x[i],w,b)
        
        d = y[i] - yact
        dw = alpha*x[i]*d
        db = alpha *d
        w = np.add(w, dw)
        b = np.add(b, db)
        print("After Iteration", i +1,":weights")
        print(w)
        print("Bias:",b)
    return w
```


```python
def per_predict(x,w,b):
    z = x * w
    tx = b + sum(z)
    #tx = sum(z)
    y = f(tx)
    return y
```


```python
def f(x):
    if(x>0):
        return 1
    elif (x <0):
        return -1
    else:
        return 0
```


```python
trainx=np.array([[1,1],[1,-1],[-1,1],[-1,-1]])
trainy=np.array([-1,1,1,-1])
testx=np.array([[1,1],[1,-1],[-1,1],[-1,-1]])
wt=np.array([0,0])
print("+++++++++")
for i in range(1,5):
  print("Epoch#",i)
  wt=percept_train(trainx,trainy,wt)
print("Final Weights:")
print(wt)
for x in testx:
  out=per_predict(x,wt,b)
  print("Input:",x)
  print("Output:",out)
```

    +++++++++
    Epoch# 1
    After Iteration 1 :weights
    [-1 -1]
    Bias: -1
    After Iteration 2 :weights
    [ 1 -3]
    Bias: 1
    After Iteration 3 :weights
    [-1 -1]
    Bias: 3
    After Iteration 4 :weights
    [1 1]
    Bias: 1
    Epoch# 2
    After Iteration 1 :weights
    [-1 -1]
    Bias: -1
    After Iteration 2 :weights
    [ 1 -3]
    Bias: 1
    After Iteration 3 :weights
    [-1 -1]
    Bias: 3
    After Iteration 4 :weights
    [1 1]
    Bias: 1
    Epoch# 3
    After Iteration 1 :weights
    [-1 -1]
    Bias: -1
    After Iteration 2 :weights
    [ 1 -3]
    Bias: 1
    After Iteration 3 :weights
    [-1 -1]
    Bias: 3
    After Iteration 4 :weights
    [1 1]
    Bias: 1
    Epoch# 4
    After Iteration 1 :weights
    [-1 -1]
    Bias: -1
    After Iteration 2 :weights
    [ 1 -3]
    Bias: 1
    After Iteration 3 :weights
    [-1 -1]
    Bias: 3
    After Iteration 4 :weights
    [1 1]
    Bias: 1
    Final Weights:
    [1 1]
    Input: [1 1]
    Output: 1
    Input: [ 1 -1]
    Output: 1
    Input: [-1  1]
    Output: 1
    Input: [-1 -1]
    Output: -1
    


```python

```
