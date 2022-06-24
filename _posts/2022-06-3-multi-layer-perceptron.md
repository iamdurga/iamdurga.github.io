---
title:  "Multilayer Percepron Using XOR function from Scratch"
date:   2022-05-26 09:29:17 +0545
categories: Machine Learing
tags:
  - Neural Network
  - Python
  
header:
  teaser: "assets/header_images/neural_network.png"
  overlay_image: "assets/header_images/neural_network.png"
toc: true
---
# Multilayer Perceptron (MLP) 

**In this blog we are going to share how non-linear problem like XOR can be solve using multiliayer perceptron. We already written blog about how to apply multilayer perceptron on majority function[ please have a look here.]( https://dataqoil.com/2022/06/17/multilayer-perce…ion-from-scratch/)** 

We all are familiar in that single layer perceptron (slp) are commonly used to classify problems that are linearly separable. If we choose a single layer perceptron for a non-linearly separable problem, the results may not be as fruitful as we expect. As a result, we must look for an alternative solution to a non-linear problem, and one such solution is the multilayer perceptron. Because AND and OR like linearly separable problem, a single layer perceptron is adequate to used. However, the problem which we can not solve linearly like XOR, thus we employed multi layer back propagation to solve it. 

## Forward- propagation

The network's synaptic weights are fixed in this phase, and the input signal is propagated layer by layer through the network until it reaches the output. As a result, alterations in this phase are limited to the activation potentials and outputs of the network's neurons. 

### Algorithm
* Initialize all weights and biases in the network
* While termination conditions is not satisfied 
* For each training tuple X in D
* For each input layer unit j: yj = xj. Output of an input unit is its actual input value
* For each hidden or output unit j, compute the net input of unit j with respect to the previous layer,
$$v_j = \sum(w_{ji} y_i) $$ compute the output of each unit j. $$ y_i = \frac{1}{1 + e^{-vj}}$$

## Back- Propagation
The back-propagation algorithm is a popular approach for training multilayer perceptrons. There are two stages to the training of MLP.

* Forward Phase
* Backward Phase

**Forward Phase**  
The network's synaptic weights are fixed in this phase, and the input signal is propagated layer by layer through the network until it reaches the output. As a result, alterations in this phase are limited to the activation potentials and outputs of the network's neurons.

**Backward Phase**
An error signal is generated in this step by comparing the network's output to a desired response. The ensuing error signal is then propagated backwards, layer by layer, via the network. During the second phase, the network's synaptic weights are gradually adjusted. 


### Algorithm

Forward algorithm is same as I wrote in single layer perceptron. Back propagation algorithm can be given below.
* The error signal at the output of neuron j at iteration n is given by
$$ e_j(n) = d_j(n) - y_j(n) $$ where dj(n) is actual output and yj(n) is predicted output By MLP

* The total error energy E(n) for all the neurons in the output layer is therefore
$$ E(n) = \frac{1}{2} \sum(e_j^2(n))$$

Where c is the set of neuron in the output layer.

* Let N be the total number of training vectors (examples). Then the average squared error is
$$ E_{avg} = \frac{1}{2} \sum_{n=1}^{N} E(n) $$

* Consider the neuron j the local field vj(n) and output yj(n) of neuron j is given by
$$ vj(n) = \sum_{i=1}^{m} wji(n)yi(n) $$
$$ yj(n) = \phi_j(v_j(n))$$ where y_j is output of neuron i and w_ji is weight of link from i to j.

* The correction $$ \Delta w_{ij}(n) $$ made to the weight is proportional to the partial derivative  $$\frac{ \delta(E)}{\delta(w_{ji}})$$ of instantaneous error

Using the chain rule of calculus, this gradient can be expressed as follows

$$ \frac{\delta E}{\delta w_{ij}} = \frac{\delta E(n)}{\delta e_j(n)} \frac{\delta e_j(n)}{\delta y_j(n)} \frac{\delta y_j(n)}{\delta v_j(n)} \frac{\delta v_j(n)}{\delta w_{ji}}....(1)$$ 

* We can get the following partial derivatives
$$ \frac{\delta E(n)}{\delta e_j(n)} = e_j(n)$$  $$ \frac{\delta e_j(n)}{\delta y_j(n)} = -1 $$ 
$$ \frac{\delta y_j(n)}{\delta v_j(n)} = \phi'_j(v_j(n)) $$ $$  \frac{\delta v_j(n)}{\delta w_{ji}} = y_i(n)$$

Putting all partial derivatives in equation 1 we get,

$$ \frac{\delta E}{\delta w_{ij}} =  - e_j(n)\phi'_j(v_j(n))  y_i(n).....(2)$$

Correction factor 
$$ \Delta w_{ij} = \alpha \frac{\delta E}{\delta w_{ij}} .....(3)$$  
 
Using equation (2) and (3) we can write,
$$ \Delta w_{ij} = - \alpha e_j(n)\phi'_j(v_j(n))  y_i(n)......(4) $$

This can be written as, 
$$ \delta w_{ij} = \alpha \delta y_j(n)$$ Where $$ \delta_j(n) = e_j(n)\phi'_j(v_j(n))......(5)$$

* The error term in equation 4 and 5 depends upon location of neuron in the MLP.



## Implementation of multilayer perceptron for XOR problem from scratch


```python
# Training of XOR function using Backpropagation
import numpy as np 
def sigmoid (x):
    return 1/(1 + np.exp(-x))
```


```python
def sigmoid_derivative(x):
    return x * (1 - x)
```


```python
#Input datasets
x = np.array([[0,0],[0,1],[1,0],[1,1]])
t = np.array([[0],[1],[1],[0]])
x.shape,t.shape
```




    ((4, 2), (4, 1))



Set the epoch to the desired outcome and the learning parameter to the same value.


```python
epochs = 100000
lr = 0.01
```

Here, we are going to use multilayer perceptron of size 2,2,1. That means 2 input node in input layer one hidden layers of size 2 and output layer.


```python
ILNeurons, HLNeurons, OLNeurons = 2,2,1
```

Initialization of weight and bias for respective layer.


```python
#Random weights and bias initialization
wh = np.random.uniform(size=(ILNeurons,HLNeurons))
#print(wh)
bh =np.random.uniform(size=(1,HLNeurons))
wo = np.random.uniform(size=(HLNeurons,OLNeurons))
#print(wo)
bo = np.random.uniform(size=(1,OLNeurons))
```

## Forward Training


```python
#Training algorithm
for i in range(epochs):
    #Forward Propagation
    vh= np.dot(x,wh)
    vh = vh+bh
    yh = sigmoid(vh)

    vo = np.dot(yh,wo)
    vo = vo+bo
    yo = sigmoid(vo)
```

## Backward Training
### Backward training can be done into two way
 
**Case I: Neuron j is output layer neuron** The neuron j's desired response dj(n) is directly available. In this example, calculating the error ej(n) is trivial. To determine the weight update term, we can utilize equations 4 or 5.
 
**case II: Neuron j is hidden layer neuron** Neuron j does not have any desirable responses. A hidden neuron's error signal must be calculated recursively in terms of the error signals of all neurons connected to it, as shown below.
 
 $$ \delta_j(n) = \phi'_j(v_j(n)) \sum_{k} \delta_k(n) w_{kj}(n)$$


```python
#Training algorithm
for i in range(epochs):
    #Forward Propagation
    vh= np.dot(x,wh)
    vh = vh+bh
    yh = sigmoid(vh)

    vo = np.dot(yh,wo)
    vo = vo+bo
    yo = sigmoid(vo)

    #Backward propagation
    error = t - yo
    deltao = error * sigmoid_derivative(yo)
    hidden_error = deltao.dot(wo.T)
    deltah = hidden_error * sigmoid_derivative(yh)

    #Updating Weights and Biases
    wo += yh.T.dot(deltao) *lr
    bo += np.sum(deltao,axis=0,keepdims=True) *lr
    wh += x.T.dot(deltah)*lr
    bh += np.sum(deltah,axis=0,keepdims=True) *lr

print("Final hidden weights: ",end='')
print(*wh)
print("Final hidden bias: ",end='')
print(*bh)
print("Final output weights: ",end='')
print(*wo)
print("Final output bias: ",end='')
print(*bo)

print("\nOutput from neural network after 10,000 epochs: ",end='')
print(*yo)

```

    Final hidden weights: [5.81424148 3.65030952] [5.79863503 3.64731901]
    Final hidden bias: [-2.4062392  -5.58225138]
    Final output weights: [7.40755241] [-8.04340317]
    Final output bias: [-3.32739567]
    
    Output from neural network after 10,000 epochs: [0.06037213] [0.94396036] [0.94401095] [0.06078971]
    


```python

```
