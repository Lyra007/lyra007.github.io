---
layout: learn
title: learn machine learning based on tensorflow
date: 2018-03-02 15:43:33 +0800
categories: learning
tags: ml,python
keywords: python
---

# Learning Machine Learning in March

https://developers.google.com/machine-learning/crash-course/

## Prerequisites

## normal class

### Framing
Terminology: 
- label: target tried to predict y
- features: input variables describing our data {x1, x2 ....}
- Labeled example: used to train the model, <mark>labeled examples: {features, label}: (x, y)</mark>
- Unlabled example: used to make predictions on new data <mark>unlabeled examples: {features, ?}: (x, ?)</mark>
- Model: used to predict labels, defined by internal parameters, which are learned 
- <bold>Training</bold> means creating or learning the model. <bold>Inference</bold> means applying the trained model to unlabeled examples.
- A regression model predicts continuous values. Eg, What is the value of a house in California?
- A classification model predicts discrete values. Eg, Is a given email message spam or not spam?

### Descending into ML

### Reducing Loss



Learning rate: a hype params that you could decide

1. Gradient descent(梯度下降法)

	weight initialization:
		convex: think of a bowel shape, just one minimum, can start anywhere 
		foreshadowing: not true for neutral nets
			* Non-convex d: think of an egg crate, more than one minimumm, strong dependency on initial value

2. Stochastic gradient descent(随机梯度下降法)
In order to get the right gradient on average for much less computation, we use Stochastic gradient descent (SGD) to the extreme. The term "stochastic" indicates that the one example comprising each batch is chosen at random.

3. Mini-Batch gradient descent: intermediate solution, batch of 10-1000


![tf_api](/img/blog/tf_api.png "TensorFlow API Hierarchy toolkits" )

 Format of a linear regression program implemented in tf.estimator

```python

import tensorflow as tf

# Set up a linear classifier.
classifier = tf.estimator.LinearClassifier()

# Train the model on some example data.
classifier.train(input_fn=train_input_fn, steps=2000)

# Use it to predict.
predictions = classifier.predict(input_fn=predict_input_fn)


```

