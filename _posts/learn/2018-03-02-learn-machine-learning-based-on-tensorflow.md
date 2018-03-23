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