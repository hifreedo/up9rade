---
layout: post
title: Gramian Matrix [series 2]
---

# Gramian Matrix

## series 1: Gramian Matrix

Given a set V of m vectors, gram matrix G is simply the matrix of all possible inner products of V.

$$ G_{ij} = V^T_i V_j $$

T denotes the transpose.

Gram matrix plays a key role in the task of style transfer in deep neural network.

A pre-trained model, usually vgg19 is introduced into the transfer process, the reason behind using pre-trained model is, we assume a model could perform versatile categories' classification should be able to understand the content of image we give. While this assumption could be challenged as well.

And get back to gram, when compare pastiche image with the given image with a certain "style", how should the "style" of image been represented im math?

As we know, gram matrix is result from a matrix multiplying its transpose, aka every row is multiplied with every column in the matrix, we could treat this process as a way of finding correlations - bigger value multiply with bigger value gets bigger, and smaller gets smaller.

