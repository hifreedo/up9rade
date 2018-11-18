---
layout: post
title: Photorealistic Style Transfer
---

# Photorealistic Style Transfer

On this series we are going to discuss about: image-to-image translation problem.

Photorealistic style transfer aim to transfer the style from the target image meanwhile eliminate the distortion on generated image, to keep the result photorealistic, this process could be treated a special kind of image-to-image.

However, this transfer process does not need a set of training data or labelling.

Gatys et al introduce neural style transfer in 2015. 
The state-of-art works are by: 
Luan et al :Deep Photo Style Tranfer in 2017.
Li et al: A Closed-form Solution to Photorealistic Image Stylization in 2018. 

They took differenct approaches: 

Luan et al treat the style transfer as affine in color space from input to output, while Li et al reckon the tranfer should not be limited only to color, but introducing patterns from style image to output.

To achieve the color transfer:

Luan et al implemented the following: use an affine function maps the input RGB values on to the output counterparts, augmented style loss with semantic segmentation. 

Li et al take 2 steps: style transfer based on refined WCT and smoothing based on graph-based ranking algorithm.

The latter achieves much more computational efficiency than the previous.