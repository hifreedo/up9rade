---
layout: post
title: Neural Network [grade 9]
---

# Receptive Field with CNN

## grade 9: Receptive field with CNN

Following is a description cited from [wikipedia](https://en.wikipedia.org/wiki/Receptive_field):

The receptive field of an individual sensory neuron is the particular region of the sensory space (e.g., the body surface, or the visual field) in which a stimulus will modify the firing of that neuron.

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/68/Conv_layer.png/231px-Conv_layer.png">

Borrowed from neuron science, given a specific layer, receptive field is how much area could a neuron see at the input layer.

The process of calculating receptive field might be a little confusing, yet, we could make it very easy to interpret.

Let's start from convolution first, given a simple black & white image input, here for better interpreting, we flat the input, from 2 dimensions into 1 dimension.

Assume there are 8 inputs, following with 3*3 conv with stride 1, and 2*2 pooling with stride 2, then 3*3 conv with stride 1.

We may construct the network as following:

There are 5 outputs in layer 1, then 3 in layer 2 and 1 in layer3.

<img src="{{site.url}}/img/nn025.png">

This is a top down approach.

We will use bottom up approach on describing receptive field, let's start with a single neuron in layer 3. According to 3rd layer was generated from a 3*3 con with stride 1, we may decompile there are 3 neurons in front of the neuron of layer 3, this is the "receptive area" layer 3 could see on layer 2.



The convolution process is like to distill a sea into a drop of water, while calculating RF (receptive field) is just like to look a whole sea from a drop of water.

Convolution is to abstract higher level info from a picture, receptive field calculating is to figure out how many input elements could be counted in one single neuron.



<img src="{{site.url}}/img/nn026.png">

Why calculating receptive field:

cal params, save space

build net structure



[post status: in writing]