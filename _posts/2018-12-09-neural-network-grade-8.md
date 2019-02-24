---
layout: post
title: Neural Network [grade 8]
---

# Convolution with CNN

## grade 8: Convolution with CNN

There's a very comprehensive introduction on convolutional neural networks from [cs231n](http://cs231n.github.io/convolutional-networks/).

We will focus on how to implement a cnn from scratch (with numpy), and apply it on mnist dataset.

Key steps for implementation:

1. On the feed forward, the convolutional operation;
2. On the back propagation, there are couple of items significantly differentiate with deep neural network we introduced before:
   * the pooling layer, which does not have an activate function like relu/sigmoid as convolution layer;
   * the pooling layer takes a down sampling strategy on feeding forward, which means data was zipped;
   * dnn applies matrix multiplication towards each layer directly, while cnn applies sum up of convolutional operation to each layer;
   * and in a word, it's vector, participated in dnn operation, and it's tensor, participated in cnn operation.
  
We need to solve these differentiations to solve back propagation in cnn.




   



[post status: in writing]