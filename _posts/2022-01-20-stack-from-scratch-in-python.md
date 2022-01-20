---
title:  "Making a Stack Data Type in Python"
date:   2022-01-20 01:29:17 +0545
categories: DSA
tags:
  - stack
  - adt
header:
  teaser: "assets/dsa/insert_stack.png"
  overlay_image: "assets/dsa/insert_stack.png"
toc: true
---

# Making a Stack Data Type in Python

## Introduction
Stack is one of the primitive data structure that we always have to study before diving into the Data Structure and Analysis. It is an example of ADT (Abstract Data Type) [where operations are predefined](https://en.wikipedia.org/wiki/Abstract_data_type). There are some other types of ADTs also like Queue, List etc.

## Operations
For any Data Type, most common operations includes inserting a data, removing a data and retrieving a data. For a simple stack there are 3 types of operations:
* **Push**: To insert a data on the top of a stack.
* **Pop**: To remove a data from the top of a stack.
* **Top**: To retrieve a top element data.

Stack operates in a LIFO (Last in First Out) way. Which means that at anytime, the pointer will be on the top of a stack and we are only allowed to operation with a data which is pointed by a pointer. If a stack is going to use an array then its size will be fixed but if we are going to use a list, then the size will variable.

### Push Operation

Lets assume that we are using an array for the stack with the size of 6 with data, `[4 5 6 8 5 2]`. Initially, a stack will be empty and the pointer will be pointing the top of stack's data which is bottom. Now in first step, to push a data, we will push 4 in the 0th position. Then pointer moves one step upwards. On the next step, next data is inserted on the 1st position. And at last, our stack will be full. 

![]({{site.url}}/assets/dsa/insert_stack.png)

Lets write it on python.


```python
class Stack:
    def __init__(self, size):
        self.size = size
        self.storage = ["~"]*size
        self.pointer = 0
        print(f"New Stack: {self.storage}")
        print(f"Pointer at {self.pointer}.\n")
    
    def push(self, x):
        self.storage[self.pointer] = x
        print(f"New Stack: {self.storage}")
        print(f"Pointer at {self.pointer+1}.\n")
        
        self.pointer+=1
    
        
```


```python
data = [4, 5, 6, 8, 5, 2]
stack = Stack(size=6)

for x in data:
    stack.push(x)
```

    New Stack: ['~', '~', '~', '~', '~', '~']
    Pointer at 0.
    
    New Stack: [4, '~', '~', '~', '~', '~']
    Pointer at 1.
    
    New Stack: [4, 5, '~', '~', '~', '~']
    Pointer at 2.
    
    New Stack: [4, 5, 6, '~', '~', '~']
    Pointer at 3.
    
    New Stack: [4, 5, 6, 8, '~', '~']
    Pointer at 4.
    
    New Stack: [4, 5, 6, 8, 5, '~']
    Pointer at 5.
    
    New Stack: [4, 5, 6, 8, 5, 2]
    Pointer at 6.
    
    

Now we have inserted the data into our stack but what if we inserted more data than the size of a stack? In that case, a overflow will happen and in above example, we have used a list as an storage and it will also show error if we tried to insert something.


```python
stack.push(0)
```


    ---------------------------------------------------------------------------

    IndexError                                Traceback (most recent call last)

    <ipython-input-23-c549502547a3> in <module>
    ----> 1 stack.push(0)
    

    <ipython-input-21-dfbe390820f6> in push(self, x)
          8 
          9     def push(self, x):
    ---> 10         self.storage[self.pointer] = x
         11         print(f"New Stack: {self.storage}")
         12         print(f"Pointer at {self.pointer+1}.\n")
    

    IndexError: list assignment index out of range


Which is expected but we must make error looking little bit different in our case.


```python
class Stack:
    def __init__(self, size):
        self.size = size
        self.storage = ["~"]*size
        self.pointer = 0
        print(f"New Stack: {self.storage}")
        print(f"Pointer at {self.pointer}.\n")
    
    def push(self, x):
        try:
            self.storage[self.pointer] = x
            print(f"New Stack: {self.storage}")
            print(f"Pointer at {self.pointer+1}.\n")

            self.pointer+=1
        except IndexError as e:
            print(f"Overflow Occured at pointer: {self.pointer}")
        
```


```python
data = [4, 5, 6, 8, 5, 2, 0]
stack = Stack(size=6)

for x in data:
    stack.push(x)
```

    New Stack: ['~', '~', '~', '~', '~', '~']
    Pointer at 0.
    
    New Stack: [4, '~', '~', '~', '~', '~']
    Pointer at 1.
    
    New Stack: [4, 5, '~', '~', '~', '~']
    Pointer at 2.
    
    New Stack: [4, 5, 6, '~', '~', '~']
    Pointer at 3.
    
    New Stack: [4, 5, 6, 8, '~', '~']
    Pointer at 4.
    
    New Stack: [4, 5, 6, 8, 5, '~']
    Pointer at 5.
    
    New Stack: [4, 5, 6, 8, 5, 2]
    Pointer at 6.
    
    Overflow Occured at pointer: 6
    

### Pop Operation
Now we have our stack fully filled, lets remove values from it. The pop operation again works with data located on pointer's position.


```python
class Stack:
    def __init__(self, size):
        self.size = size
        self.storage = ["~"]*size
        self.pointer = 0
        print(f"New Stack: {self.storage}")
        print(f"Pointer at {self.pointer}.\n")
    
    def push(self, x):
        try:
            self.storage[self.pointer] = x
            print(f"New Stack: {self.storage}")
            print(f"Pointer at {self.pointer+1}.\n")

            self.pointer+=1
        except IndexError as e:
            print(f"Overflow Occured at pointer: {self.pointer} \n")
    
    def pop(self):
        self.storage = self.storage[:-1]
        
        print(f"New Stack: {self.storage}")
        print(f"Pointer at {self.pointer-1}.\n")
        
        self.pointer-=1
```


```python
data = [4, 5, 6, 8, 5, 2, 0]
stack = Stack(size=6)

for x in data:
    stack.push(x)
stack.pop()
```

    New Stack: ['~', '~', '~', '~', '~', '~']
    Pointer at 0.
    
    New Stack: [4, '~', '~', '~', '~', '~']
    Pointer at 1.
    
    New Stack: [4, 5, '~', '~', '~', '~']
    Pointer at 2.
    
    New Stack: [4, 5, 6, '~', '~', '~']
    Pointer at 3.
    
    New Stack: [4, 5, 6, 8, '~', '~']
    Pointer at 4.
    
    New Stack: [4, 5, 6, 8, 5, '~']
    Pointer at 5.
    
    New Stack: [4, 5, 6, 8, 5, 2]
    Pointer at 6.
    
    Overflow Occured at pointer: 6 
    
    New Stack: [4, 5, 6, 8, 5]
    Pointer at 5.
    
    

Now that we have made a pop operation, what happens if our stack is empty and we tried to remove a data? That case is a stack underflow. Lets write that also.


```python
for i in range(len(data)):
    stack.pop()
```

    New Stack: [4, 5, 6, 8]
    Pointer at 4.
    
    New Stack: [4, 5, 6]
    Pointer at 3.
    
    New Stack: [4, 5]
    Pointer at 2.
    
    New Stack: [4]
    Pointer at 1.
    
    New Stack: []
    Pointer at 0.
    
    New Stack: []
    Pointer at -1.
    
    New Stack: []
    Pointer at -2.
    
    

In above code, no error is shown when pointer becomes -ve. Lets assume that if pointer is already 0 and we tried to remove, then it should be an error.


```python
class Stack:
    def __init__(self, size):
        self.size = size
        self.storage = ["~"]*size
        self.pointer = 0
        print(f"New Stack: {self.storage}")
        print(f"Pointer at {self.pointer}.\n")
    
    def push(self, x):
        try:
            self.storage[self.pointer] = x
            print(f"New Stack: {self.storage}")
            print(f"Pointer at {self.pointer+1}.\n")

            self.pointer+=1
        except IndexError as e:
            print(f"Overflow Occured at pointer: {self.pointer} \n")
    
    def pop(self):
        if self.pointer<1:
            print("Stack Underflow occured.")
        else:
            self.storage = self.storage[:-1]
            print(f"New Stack: {self.storage}")
            print(f"Pointer at {self.pointer-1}.\n")

            self.pointer-=1
        
```


```python
data = [4, 5, 6, 8, 5, 2, 0]
stack = Stack(size=6)

for x in data:
    stack.push(x)
stack.pop()

for i in range(len(data)):
    stack.pop()
```

    New Stack: ['~', '~', '~', '~', '~', '~']
    Pointer at 0.
    
    New Stack: [4, '~', '~', '~', '~', '~']
    Pointer at 1.
    
    New Stack: [4, 5, '~', '~', '~', '~']
    Pointer at 2.
    
    New Stack: [4, 5, 6, '~', '~', '~']
    Pointer at 3.
    
    New Stack: [4, 5, 6, 8, '~', '~']
    Pointer at 4.
    
    New Stack: [4, 5, 6, 8, 5, '~']
    Pointer at 5.
    
    New Stack: [4, 5, 6, 8, 5, 2]
    Pointer at 6.
    
    Overflow Occured at pointer: 6 
    
    New Stack: [4, 5, 6, 8, 5]
    Pointer at 5.
    
    New Stack: [4, 5, 6, 8]
    Pointer at 4.
    
    New Stack: [4, 5, 6]
    Pointer at 3.
    
    New Stack: [4, 5]
    Pointer at 2.
    
    New Stack: [4]
    Pointer at 1.
    
    New Stack: []
    Pointer at 0.
    
    Stack Underflow occured.
    Stack Underflow occured.
    

Now tweaking it little bit more to make it more readable.


```python
class Stack:
    def __init__(self, size):
        self.size = size
        self.storage = ["~"]*size
        self.pointer = 0
        print(f"New Stack: {self.storage}")
        print(f"Pointer at {self.pointer}.\n")
    
    def push(self, x):
        print("=" * 20+" Push Operation "+"=" * 20)
        try:
            self.storage[self.pointer] = x
            print(f"New Stack: {self.storage}")
            print(f"Pointer at {self.pointer+1}.")

            self.pointer+=1
        except IndexError as e:
            print(f"Overflow Occured at pointer: {self.pointer}")
        print("="*55 + "\n")
        
    def pop(self):
        print("=" * 20+" Pop Operation "+"=" * 20)
        if self.pointer<1:
            print("Stack Underflow occured.")
        else:
            self.storage = self.storage[:-1]
            print(f"New Stack: {self.storage}")
            print(f"Pointer at {self.pointer-1}.")

            self.pointer-=1
        print("="*55 + "\n")
        
```


```python
data = [4, 5, 6, 8, 5, 2, 0]
stack = Stack(size=6)

for x in data:
    stack.push(x)
stack.pop()

for i in range(len(data)):
    stack.pop()
```

    New Stack: ['~', '~', '~', '~', '~', '~']
    Pointer at 0.
    
    ==================== Push Operation ====================
    New Stack: [4, '~', '~', '~', '~', '~']
    Pointer at 1.
    =======================================================
    
    ==================== Push Operation ====================
    New Stack: [4, 5, '~', '~', '~', '~']
    Pointer at 2.
    =======================================================
    
    ==================== Push Operation ====================
    New Stack: [4, 5, 6, '~', '~', '~']
    Pointer at 3.
    =======================================================
    
    ==================== Push Operation ====================
    New Stack: [4, 5, 6, 8, '~', '~']
    Pointer at 4.
    =======================================================
    
    ==================== Push Operation ====================
    New Stack: [4, 5, 6, 8, 5, '~']
    Pointer at 5.
    =======================================================
    
    ==================== Push Operation ====================
    New Stack: [4, 5, 6, 8, 5, 2]
    Pointer at 6.
    =======================================================
    
    ==================== Push Operation ====================
    Overflow Occured at pointer: 6
    =======================================================
    
    ==================== Pop Operation ====================
    New Stack: [4, 5, 6, 8, 5]
    Pointer at 5.
    =======================================================
    
    ==================== Pop Operation ====================
    New Stack: [4, 5, 6, 8]
    Pointer at 4.
    =======================================================
    
    ==================== Pop Operation ====================
    New Stack: [4, 5, 6]
    Pointer at 3.
    =======================================================
    
    ==================== Pop Operation ====================
    New Stack: [4, 5]
    Pointer at 2.
    =======================================================
    
    ==================== Pop Operation ====================
    New Stack: [4]
    Pointer at 1.
    =======================================================
    
    ==================== Pop Operation ====================
    New Stack: []
    Pointer at 0.
    =======================================================
    
    ==================== Pop Operation ====================
    Stack Underflow occured.
    =======================================================
    
    ==================== Pop Operation ====================
    Stack Underflow occured.
    =======================================================
    
    

### Top Operation
This is a simple operation. It gives the value that is below the position currently pointed by a pointer.


```python
class Stack:
    def __init__(self, size):
        self.size = size
        self.storage = ["~"]*size
        self.pointer = 0
        print(f"New Stack: {self.storage}")
        print(f"Pointer at {self.pointer}.\n")
    
    def push(self, x):
        print("=" * 20+" Push Operation "+"=" * 20)
        try:
            self.storage[self.pointer] = x
            print(f"New Stack: {self.storage}")
            print(f"Pointer at {self.pointer+1}.")

            self.pointer+=1
        except IndexError as e:
            print(f"Overflow Occured at pointer: {self.pointer}")
        print("="*55 + "\n")
        
    def pop(self):
        print("=" * 20+" Pop Operation "+"=" * 20)
        if self.pointer<1:
            print("Stack Underflow occured.")
        else:
            self.storage = self.storage[:-1]
            print(f"New Stack: {self.storage}")
            print(f"Pointer at {self.pointer-1}.")

            self.pointer-=1
        print("="*55 + "\n")
    
    def top(self):
        print("=" * 20+" Top Operation "+"=" * 20)
        try:
            print(f"Pointer at {self.pointer}.")
            print(f"Return: {self.storage[self.pointer-1]}")
        except:
            print("Nothing on the top. Stack is empty.")
        print("="*55 + "\n")
    
```


```python
data = [4, 5, 6, 8, 5, 2, 0]
stack = Stack(size=6)

for x in data:
    stack.push(x)
    stack.top()
stack.pop()

for i in range(len(data)):
    stack.pop()
    stack.top()
```

    New Stack: ['~', '~', '~', '~', '~', '~']
    Pointer at 0.
    
    ==================== Push Operation ====================
    New Stack: [4, '~', '~', '~', '~', '~']
    Pointer at 1.
    =======================================================
    
    ==================== Top Operation ====================
    Pointer at 1.
    Return: 4
    =======================================================
    
    ==================== Push Operation ====================
    New Stack: [4, 5, '~', '~', '~', '~']
    Pointer at 2.
    =======================================================
    
    ==================== Top Operation ====================
    Pointer at 2.
    Return: 5
    =======================================================
    
    ==================== Push Operation ====================
    New Stack: [4, 5, 6, '~', '~', '~']
    Pointer at 3.
    =======================================================
    
    ==================== Top Operation ====================
    Pointer at 3.
    Return: 6
    =======================================================
    
    ==================== Push Operation ====================
    New Stack: [4, 5, 6, 8, '~', '~']
    Pointer at 4.
    =======================================================
    
    ==================== Top Operation ====================
    Pointer at 4.
    Return: 8
    =======================================================
    
    ==================== Push Operation ====================
    New Stack: [4, 5, 6, 8, 5, '~']
    Pointer at 5.
    =======================================================
    
    ==================== Top Operation ====================
    Pointer at 5.
    Return: 5
    =======================================================
    
    ==================== Push Operation ====================
    New Stack: [4, 5, 6, 8, 5, 2]
    Pointer at 6.
    =======================================================
    
    ==================== Top Operation ====================
    Pointer at 6.
    Return: 2
    =======================================================
    
    ==================== Push Operation ====================
    Overflow Occured at pointer: 6
    =======================================================
    
    ==================== Top Operation ====================
    Pointer at 6.
    Return: 2
    =======================================================
    
    ==================== Pop Operation ====================
    New Stack: [4, 5, 6, 8, 5]
    Pointer at 5.
    =======================================================
    
    ==================== Pop Operation ====================
    New Stack: [4, 5, 6, 8]
    Pointer at 4.
    =======================================================
    
    ==================== Top Operation ====================
    Pointer at 4.
    Return: 8
    =======================================================
    
    ==================== Pop Operation ====================
    New Stack: [4, 5, 6]
    Pointer at 3.
    =======================================================
    
    ==================== Top Operation ====================
    Pointer at 3.
    Return: 6
    =======================================================
    
    ==================== Pop Operation ====================
    New Stack: [4, 5]
    Pointer at 2.
    =======================================================
    
    ==================== Top Operation ====================
    Pointer at 2.
    Return: 5
    =======================================================
    
    ==================== Pop Operation ====================
    New Stack: [4]
    Pointer at 1.
    =======================================================
    
    ==================== Top Operation ====================
    Pointer at 1.
    Return: 4
    =======================================================
    
    ==================== Pop Operation ====================
    New Stack: []
    Pointer at 0.
    =======================================================
    
    ==================== Top Operation ====================
    Pointer at 0.
    Nothing on the top. Stack is empty.
    =======================================================
    
    ==================== Pop Operation ====================
    Stack Underflow occured.
    =======================================================
    
    ==================== Top Operation ====================
    Pointer at 0.
    Nothing on the top. Stack is empty.
    =======================================================
    
    ==================== Pop Operation ====================
    Stack Underflow occured.
    =======================================================
    
    ==================== Top Operation ====================
    Pointer at 0.
    Nothing on the top. Stack is empty.
    =======================================================
    
    

## Conclusion

Thank you for reading this blog and reaching to the end. In the next blog, I will share similar approach for the Queue and it will also be a fun to try.