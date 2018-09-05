---
layout: post
title: What is image file [grade 1]
---

# What Is An Image File (JPEG)

Almost all of the image files we are dealing with through machine learning, there are not in there "original or raw" format, in other words, they have be compressed or transformed into certain file format.

One of the commonly used image file format is ".jpeg" or ".jpg", which usually could achieve 10:1 compression rate without sacrifice too much on the quality.

The magic of JPEG compression behind is: human vision is more sensitive to color or brightness variations in large areas than to the high frequency brightness variations. Which means we could discard some info in high frequency areas.

To have a detailed understand about JPEG formating, following are some key methodologies: 

* Huffman Coding
* Entropy Encoding
* Discrete Cosine Transform (DCT)

JPEG is widely used in internet, while with the era of "5g" reaching, lossless data compression maybe will change current regime, still is interesting to know more about the source of our deep learning models' training material.

JPEG was released in 1992 (approved by ISO in 1994), and from 2017, apple iOS, macOS, watchOS, tvOS started to support a new image format: HEIF.

# High Efficiency Image File format (HEIF)

HEIF is a container format (approved by ISO in 2015), it can contain still images and image collections, image bursts, image sequences, image derivations and auxiliary image storage. HEIF supports rectangular cropping and rotation by 90, 180, 270, as you may guess out, the purpose is to adapt to photography scenario, to enable manually adjust image or image sequence orientation without re-encoding image itself. This feature provides a lot computational efficiency.

According to the HEIF format developer, that twice as much information can be stored in HEIF image as compared to a JPEG image in the same size, with even better quality. On the compression performance, also benchmark was released as: JPEG would require 2.39 times file size in order to achieve same picture quality to HEIF.

HEIF is implemented by:

Context-adaptive Binary Arithmetic Coding (CABAC), a form of entropy encoding, a lossless compression technique.

HEIF might be the next trend for images through internet.

[post status: half done]