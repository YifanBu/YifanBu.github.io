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

# Python for Data Science

## NumPy

NumPy is a Linear Algebra Library for Python.

- one of the main building blocks of the libraries in the PyData Ecosystem.
- incredibly fast

`conda install numpy`

### NumPy Arrays

### NumPy Indexing and Selection

NumPy arrays differ from a normal Python list because of their ability to **broadcast**:

```python
arr = np.arange(0,11) #array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10])

arr[0:5]=100 #array([100, 100, 100, 100, 100,   5,   6,   7,   8,   9,  10])
```

Indexing a 2D array(matrices):

```python

```

Fancy Indexing:

Fancy indexing allows you to select entire rows or columns out of order,to show this, let's quickly build out a numpy array:

### NumPy Operations

Universal Array Functions



## Pandas

Pandas is an open source library that built on top of NumPy.

- fast analysis
- data cleaning and preparation
- excels in performance and productivity
- has built-in visualization features
- can work with data from a wide variety of sources

`conda install pandas`

### Series

A Series is very similar to a NumPy array (in fact it is built on top of the NumPy array object). 

What differentiates the NumPy array from a Series:

- a Series can have axis labels, meaning it can be indexed by a label, instead of just a number location. 
- It also doesn't need to hold numeric data, it can hold any arbitrary Python Object.

The key to using a Series is understanding its **index**. Pandas makes use of these index names or numbers by allowing for fast look ups of information (works like a hash table or dictionary).

### DataFrames

DataFrames are the workhorse of pandas. We can think of a DataFrame as a bunch of Series objects put together to share the same index.

```python
from numpy.random import randn

df = pd.DataFrame(randn(5,4), index='A B C D E'.split(), columns='W X Y Z'.split())
```

#### Selection and Indexing



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