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

