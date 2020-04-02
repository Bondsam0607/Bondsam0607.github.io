---
layout: page
title: Sentiment Analysis
tags: AI
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image: false
---

Using LSTM to apply sentiment analysis.

Five phases:

- prepare a word vector generation model
- create an ID's matrix for training set
- RNN with LSTM units
- Training
- Testing

## Word vector generator

In order to process the text, we need to tranform them to vectors.

For example, we transform a sentence with 16 words to a 16*D matrix. Each word is represented by a vector.

What we want to achieve is placing words such as "like"
and "adore" closely.

### Word2Vec Model

Word2Vec Model creates word vectors by looking at the context with which words appear in sentences. Words with similar contexts will be places close together in the vector space.

The output of a Word2Vec model is called an **embeddig matrix**.

![embedding matrix](/images/Sentiment_Analysis/SentimentAnalysis3.png)

The embedding matrix is made up of all the distinct word in the training corpus. 

## Recurrent Neural Networks(RNNs)

**Why do we choose RNNs?**

The main difference between RNN and other feedforword NNs is the temporal aspect.

Each input sequecce will be associated with a time step.

![time step](/images/Sentiment_Analysis/SentimentAnalysis18.png)

$$h_t = \sigma(W^Hh_{t-1}+W_Xx_t)$$

- The two W represent the weights which will be updated through backpropagation.
- x is the input
- The sigma is an activation function.

From the formula above, we can see that each hidden state node encapsulate and summarize all the information before. And this feature is exactly what nlp needs.

## LSTM

LSTM(Long Short Term Memory Units) are modules that you can place inside of a RNN.

![LSTMs](/images/Sentiment_Analysis/SentimentAnalysis10.png)

### Why do we need LSTM?

RNN is so simple that it's not capable of handling complex information.

