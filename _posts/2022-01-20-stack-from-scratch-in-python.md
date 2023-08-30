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
Stack is one of the primitive data structure that we have to study before diving into the Data Structure and Algorithms. It is an example of ADT (Abstract Data Type) [where operations are predefined](https://en.wikipedia.org/wiki/Abstract_data_type). There are some other types of ADTs some of them are Queue, List.

## Operation
For any Data Type, most common operation includes inserting a data, removing a data and retrieving a data. For a simple stack there are 3 types of operation:
* **Push**: To insert a data on the top of a stack.
* **Pop**: To remove a data from the top of a stack.
* **Top**: To retrieve a top element data.

A stack operates based on the Last-In-First-Out (LIFO) principle. This means that the stack pointer always resides at the top of the stack, and we can only perform operations on the data that the pointer is currently referencing. When implementing a stack using an array, the size of the stack is fixed. On the other hand, if a list is used for implementation, the stack size becomes variable.

### Push Operation

Let's consider using an array to implement a stack with a size of 6 and data [4, 5, 6, 8, 5, 2]. Initially, the stack is empty, and the pointer is positioned at the bottom of the stack's data. In the first step, we push the data 4 into the 0th position of the stack. Consequently, the pointer moves one step upward. During the subsequent step, the next data is inserted into the 1st position of the stack. This process continues until all available positions in the stack are filled. As a result, our stack becomes full. 

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
    
    

Once data is inserted into the stack, it's essential to consider the stack's size limitations. If we attempt to insert more data than the stack's allocated size, an overflow condition occurs. In the previous example, the stack was implemented using a list as storage. If we were to try inserting additional elements beyond the list's capacity, an error would occur, highlighting the limitation of the stack's available space. It's important to manage the size and capacity of the stack to avoid such overflow situations.


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
Now, when our stack is fully occupied, let's explore the process of removing values from it. The "pop" operation revolves around the data situated at the position pointed to by the stack's pointer. This operation extracts the data and adjusts the pointer accordingly.


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
    
    

Certainly, when attempting to perform a "pop" operation on an empty stack, a situation known as a "stack underflow" occurs. This scenario arises when there are no elements left in the stack to remove. It's important to handle stack underflow cases to prevent errors and ensure the proper functioning of the stack-based operations.


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
    
    

In the previous discussion, we explored the 'pop' operation that involves removing data from the stack based on the position pointed to by the stack's pointer. However, it's important to note that if the pointer is already at position 0 and an attempt is made to remove data, an error occurs. This situation is referred to as a 'stack underflow,' which arises when the stack is empty and there are no elements left to remove. Proper handling of stack underflow scenarios is crucial to ensure the integrity of stack operations.








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
    

Now tweaking it little bit more to make it readable.


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
This is a simple operation. It give the value that is below the position currently pointed by a pointer.


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

Thank you for taking the time to read this blog post to its conclusion. I'm excited to announce that my next blog will delve into a similar approach, this time focusing on queues. Exploring queues will provide another engaging learning experience. Stay tuned for the upcoming blog post—it promises to be both informative and enjoyable!