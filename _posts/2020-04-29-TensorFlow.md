---
title: "Machine Learning with TensorFlow"
date: 2020-04-29
tags: [Google Cloud, TensorFlow, Machine Learning]
header:
image:
excerpt: "Machine Learning"
toc: true
toc_label: "Table of Contents"
toc_sticky: true
toc_icon: "cog"
---

# How Google does ML

Google infuses Machine Learning into almost all its product. There are also many pre-trained machine learning services available on Google Cloud. 

Data is the fuel for ML models. ML converts examples into knowledge.

There are two stages of ML:

1. Train a ML model (a mathematical function) with examples (label + input): make tiny adjustments to model function so output is closer to label for a given input.
2. Run inference with a trained model

Data scientists must focus on both the training and inference stages of ML.

Training deep neural networks required computing power. For machine learning, you need to build a **streaming** pipeline in addition to a **batch** pipeline.


## AI Platform Notebooks

Increasingly, data analysis and ML are carried out in self-descriptive, shareable, executable notebooks.

## TensorFlow Playground

TensorFlow Playground is a powerful tool for visualizing how neural networks work.

# ML with TensorFlow

## What is TensorFlow

TensorFlow is an open-source high-performance library for numerical computation that uses direct graphs.

A DAG consists of tensors and operations on those tensors. A tensor is an N-dimensional array of data.

TensorFlow is popular among both deep learning researchers and machine learning engineers.

## TensorFLow API 

The Core TensorFlow Python API gives users full control to build and run. 

*tf.layers*, *tf.losses*, *tf.metrics* provide components useful when building custom NN models.

*tf.estimator* is the high-level API for distributed training.

## Lazy Evaluation

TensorFlow does lazy evaluation. You write a DAG, the directed acyclic graph, and then you run the DAG in the context of a session to get results. The graph definition is separate from the training loop because this is a lazy evaluation model. 

First step, create the graph:

```python
c = tf.add(a, b)
```

Second step, run the graph:

```python
session = tf.Session()
numpy_c = session.run(c, feed_dict= ...)
```


## Graph and Session

Graphs can be processed, compiles, remotely executed, and assigned to devices.

```python
import tensorflow as tf

x = tf.constant([3, 5, 7])
y = tf.constant([1, 2, 3])

with tf.Session() as sess:
  print sess.run(z)
```

## Tensor and Variables

### Tensors

A tensor is an N-dimensional array of data. When you create a tensor, you typically specify its shape.

Tensors can be sliced:

```python
import tensorflow as tf

x = tf.constant([[3, 5, 7],[4, 6, 8]])
y = x[:, 1]

with tf.Session() as sess:
  print y.eval()
```

Tensors can be reshaped:

```python
import tensorflow as tf

x = tf.constant([[3, 5, 7],[4, 6, 8]])
y = tf.reshape(x, [3, 2])

with tf.Session() as sess:
  print y.eval()
```

### Variables

A variable is a tensor whose value is initialized and then typically changed as the program runs.


## Debugging TensorFlow programs

### Steps

1. Read error messages to understand the problem
2. Isolate the method in question
3. Call the problematic method with fake data

### Common Problems

- Shape problems
- Data type problems

<!--
## The Path to ML

1. Individual contributor: prototype and try out ideas
2. Delegation: gently ramp up to include more people
3. Digitization: automate mundane parts of the process
4. Big Data and Analytics: measure and achieve data-driven success
5. Machine Learning: automated feedback loop that can outpace human scale

# Feature Engineering


# Art and Science of ML

**Evaluation Metrics** can help highlight areas where machine learning could be more inclusive.

## Loss Function

A loss function can take the quality of predictions for a group of data points from our training set and compose them into a single number, with which to estimate the quality of the model's current parameters.

## Gradient Descent

Gradient Descent refers to the process of walking down the surface formed by using the loss function on all the points in parameter space.

## Performance Metrics

Instead of searching for the perfect loss function during training, we're instead going to use a new sort of metric after training is complete. And this new sort of metric will allow us to reject models that have settled into inappropriate minima. Such metrics are called performance metrics. 

Performance metrics have two benefits over loss functions: 

Firstly, they're easier to understand. This is because they're often simple combinations of countable statistics. Secondly, performance metrics are directly connected to business goals.
-->
