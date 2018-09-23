---
layout: post
title: What is image file [grade 3]
---

# What is image file: Histogram Similarity

## grade 3: histogram similarity

Image histogram is the representation of tonal distribution in a digital image, with the horizontal axis for tonal variations, and vertical axis as number of pixels in that particular tone.

Photographers uses them as reference to check out highlights and shadows, balance of light and darkness. 
In computer vision, which could be applied to image similarity comparison, edge detection and image segmentation.

Prior to start calculate histogram, we will talk one more bit background of the "color models" about: RGB, HSV, HSL.

RGB is the adopted by display monitors as "Truecolor" and css 2.0 standard for web pages. RGB model consists of red, green and blue colors with intensities range from 0 to 255.

HSV describes colors in: hue, saturation, value(brightness). HSV model separates saturation, brightness, shades from the hue, and was adopted by Mac OS, adobe and OpenCV.

HSL model describes colors in: hue, saturation, luminance(lightness), is adopted in CSS3 and ImageMagic.

In general, HSV and HSL are more close to the way human vision perceives color making attributes.
There are more than 3 color models apply to different field, the mentioned 3 are commonly used in computer vision.

With the above background information been introduced, we are going to jump into the specific scenario:
given 2 images, if we have had the histograms calculated, how to compare the similarity?

We represent 6 different methods to compare similarities and will design a test to validate:

$$Correlation: \: d(H_1, H_2) =  \frac{\sum_i(H_1(I)-\overline{H})\sum_i(H_2(I)-\overline{H})}{\sqrt{\sum_i(H_1(I)-\overline{H})^2\sum_i(H_2(I)-\overline{H})^2}}$$

$$ Chi-Square: \: d(H_1, H_2) =  \sum_i\frac{(H_1(I)-H_2(I)^2}{H_1(I)} $$

$$ Intersection: \: d(H_1, H_2) = \sum_imin(H_1(I),H_2(I))$$

$$ Bhattacharyya \: distance: \: d(H_1, H_2) = \sqrt{1-\frac{1}{\sqrt{\overline{H_1} \: \overline{H_2} \: N^2}}\sum_i{\sqrt{H_1(I) \: H_2(I)}}} $$

$$ Cosine \: similarity: \: d(H_1, H_2) = \frac{H_1 \bullet H_2}{\begin{Vmatrix}H_1\end{Vmatrix}\begin{Vmatrix}H_2\end{Vmatrix}} $$

$$ Histogram \: similarity: \: d(H_1, H_2) = \sum\frac{|t_1 - t_2|}{max(t_1, t_2)} \: / \: len(H_1)  $$

Formula (1),(2),(3),(4) were implemented by OpenCV in compareHist function.

Next, we will construct an experiment on testing above 6 methods:

Take an image as base, it will compare to: itself, half of the base, split base into 2 parts and swap them, smaller size base, a similar image, a none related image.

We will use OpenCV to calculate histogram, and implement above methods manually.

```python

```