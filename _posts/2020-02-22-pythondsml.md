---
title: "Python for Data Science and Machine Learning"
date: 2020-02-22
tags: [Machine Learning, Data Science, Python]
header:
image:
excerpt: "Python, Data Science"
toc: true
toc_label: "Table of Contents"
toc_sticky: true
toc_icon: "cog"
---

# Python Basics

### Printing

```python
num = 12
name = 'Sam'
print('My number is: {one}, and my name is: {two}'.format(one=num,two=name))
print('My number is: {}, and my name is: {}'.format(num,name))
```

### Lists

```python
my_list = ['a','b','c']
my_list.append('d')
my_list[1:] # ['b', 'c', 'd']
my_list[:1] # ['a']

nest = [1,2,3,[4,5,['target']]]
nest[3][2] # ['target']
nest[3][2][0] # 'target'
```

### list comprehension

```python
x = [1,2,3,4]

out = []
for item in x:
    out.append(item**2)
print(out) # [1, 4, 9, 16]

[item**2 for item in x] # [1, 4, 9, 16]
```

### Dictionaries

```python
d = {'key1':'item1','key2':'item2'}
d['key1'] # 'item1'
```

### Tuples

```python
t = (1,2,3)
t[0] # 1
```

### Sets

```python
{1,2,3,1,2,1,2,3,3,3,3,2,2,2,1,1,2} # {1, 2, 3}
```

### if

```python
if 1 > 2:
    print('first')
else:
    print('last')

if 1 == 2:
    print('first')
elif 3 == 3:
    print('middle')
else:
    print('Last')
```

### for Loops

```python
seq = [1,2,3,4,5]
for item in seq:
    print(item)
```

### while Loops

```python
i = 1
while i < 5:
    print('i is: {}'.format(i))
    i = i+1
```

### range()

```python
for i in range(5):
    print(i)

list(range(5)) # [0, 1, 2, 3, 4]
```

### functions

```python
def my_func(param1='default'):
    """
    Docstring goes here.
    """
    print(param1)

def square(x):
    return x**2
```

### lambda expressions

```python
x = lambda a : a + 10
print(x(5))

x = lambda a, b : a * b
print(x(5, 6))

x = lambda a, b, c : a + b + c
print(x(5, 6, 2))
```

### map & filter

```python
seq = [1,2,3,4,5]
list(map(lambda var: var*2,seq)) # [2, 4, 6, 8, 10]
```

### methods

```python
st = 'hello my name is Sam'
st.lower()
st.upper()
st.split() # ['hello', 'my', 'name', 'is', 'Sam']


d = {'key1': 'item1', 'key2': 'item2'}
d.keys() # dict_keys(['key2', 'key1'])
d.items() # dict_items([('key2', 'item2'), ('key1', 'item1')])


lst = [1,2,3]
lst.pop() # 3
lst # [1, 2]

'x' in ['x','y','z'] # True
```

# Python for Data Science

## NumPy

NumPy is a Linear Algebra Library for Python.

- one of the main building blocks of the libraries in the PyData Ecosystem.
- incredibly fast

`conda install numpy`

### NumPy Arrays



## Pandas

Pandas is an open source library that built on top of NumPy.

- fast analysis
- data cleaning and preparation
- excels in performance and productivity
- has built-in visualization features
- can work with data from a wide variety of sources

`conda install pandas`

### Series



### DataFrames



## Matplotlib

Matplotlib is the most popular plotting library for Python. It is designed to have a similar feel to MatLab's graphical plotting.

`conda install matplotlib`

## Seaborn

Seaborn is a statistical plotting library.

- has beautiful default styles
- designed to work very well with pandas DataFrame objects

`conda install seaborn`

# Python for Machine Learning

## Linear Regression



## Logistic Regression



## K-Nearest-Neighbors



## Decision-Trees-and-Random-Forests



## Support-Vector-Machines



## K-Means-Clustering