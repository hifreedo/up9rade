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

We will use bottom up approach on describing receptive field, let's start with a single neuron in layer 3. According to 3rd layer was generated from a 3*3 con with stride 1, we may decompile there are 3 neurons in front of the neuron of layer 3, this is the "receptive area" that layer 3 could see on layer 2.

Moving on, each of the neuron connects to 2 neurons in layer 1, because the layer 2 was construct of 2*2 pooling with stride of 2.

After mapping 6 neurons to 8 neurons in input layer, we done building the network bottom up.

Now tak a look at the green neuron of layer 1, how much could it see from input layer? 3. Which means the receptive field of layer 1 is 3.

Then look at the red neuron from layer 2, how many neurons could it see from the input layer? 4, the receptive field in layer 2 is 4.

Finally, how many could neuron in layer 3 see? 8, the receptive field in layer 3 is 8. Layer 3 could see 3 in layer 2, and see 6 in layer 1, and see 8 in input layer.

The receptive field is not that hard to interpret.

The convolution process is like to distill a sea into a drop of water, while calculating RF (receptive field) is just like to look a whole sea from a drop of water.

Convolution is to abstract higher level info from a picture, receptive field calculating is to figure out how many input elements could be counted in one single neuron.

<img src="{{site.url}}/img/nn026.png">

Now, what's it for calculating receptive field?

1. Calculate parameters in a network, make the network less computation but maintain the similar representation power. Look at the network, with a 3*3 conv then 2*2 pooling then 3*3 conv, we could see which has same power of 8*8 conv.
2. While on build up a network for classification task, we pay attention to the receptive field in the deepest layer, could it see the whole picture of the input? If not, the performance will be impacted due to receptive field is not big enough.





[post status: in writing]