---
layout: page
title: Epoch,Iteration and Batch
tags: AI
excerpt_separator: <!--more-->
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image: false
---

When it comes to training a model, *Epoch*,*Iteration* and *Batch* are often confusing. What do these three words really mean?

<!--more-->

## Epoch

One epoch is a process of feeding an ENTIRE dataset into a model.

### Why multiple times?

If we train the model using only one epoch, it mostly turns out underfitting.

If we train more, it will be optimium and then overfitting.

*One example is Gradient Descent which is iterative which means that we need to get the results multiple times to get the optimal result.*

## Batch

When we are feeding a dataset into a model, it is mostly too big for the model. So we need to split the training data into several parts which is called **Batch**. 

### Batch Size

Batch size means how many training examples are there in a batch.

## Iteration

Iterations is the number of batches you need for one epoch.

$$Iteration = \frac{one\_epoch}{Batch\_size}$$


*source: [Epoch vs Batch Size vs Iterations by SAGAR SHARMA
](https://towardsdatascience.com/epoch-vs-iterations-vs-batch-size-4dfb9c7ce9c9)*