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

$$Correlation: \: d(H_1, H_2) =  \frac{\sum_i(H_1(I)-\overline{H_1})(H_2(I)-\overline{H_2})}{\sqrt{\sum_i(H_1(I)-\overline{H})^2\sum_i(H_2(I)-\overline{H})^2}}$$

$$ Chi-Square: \: d(H_1, H_2) =  \sum_i\frac{(H_1(I)-H_2(I))^2}{H_1(I)} $$

$$ Intersection: \: d(H_1, H_2) = \sum_imin(H_1(I),H_2(I))$$

$$ Bhattacharyya \: distance: \: d(H_1, H_2) = \sqrt{1-\frac{1}{\sqrt{\overline{H_1} \: \overline{H_2} \: N^2}}\sum_i{\sqrt{H_1(I) \: H_2(I)}}} $$

$$ Cosine \: similarity: \: d(H_1, H_2) = \frac{H_1 \bullet H_2}{\begin{Vmatrix}H_1\end{Vmatrix}\begin{Vmatrix}H_2\end{Vmatrix}} $$

$$ Histogram \: similarity: \: d(H_1, H_2) = \sum\frac{|t_1 - t_2|}{max(t_1, t_2)} \: / \: len(H_1)  $$

Formula (1),(2),(3),(4) were implemented by OpenCV in compareHist function.

Next, we will construct an experiment on testing above 6 methods:

Take an image as base, it will compare to: itself, half of the base, split base into 2 parts and swap them, a similar image, a none related image. All these images are in same height & width, but not necessary to be in square shape.

We will use OpenCV to calculate histogram, and implement above methods manually.

```python
# histogram similarity calculation
# with rgb to gray formats
# manually implemented similarity calculation functions

import cv2 as cv
import numpy as np
%matplotlib inline
from matplotlib import pyplot as plt

# load image
src_base = cv.imread("dataset/base.jpg")
src_test0 = cv.imread("dataset/base_swap.jpg")
src_test1 = cv.imread("dataset/test1.jpg")
src_test2 = cv.imread("dataset/test2.jpg")

# convert to gray format
gray_test0 = cv.cvtColor(src_test0, cv.COLOR_BGR2GRAY)
gray_test1 = cv.cvtColor(src_test1, cv.COLOR_BGR2GRAY)
gray_test2 = cv.cvtColor(src_test2, cv.COLOR_BGR2GRAY)
gray_base = cv.cvtColor(src_base, cv.COLOR_BGR2GRAY)

# create a test image as half of base image
gray_test3 = gray_base[gray_base.shape[0]//2:,:]

# histogram calculation
histSize = [256]
ranges = [0, 256]
hist_base = cv.calcHist([gray_base], [0], None, histSize, ranges)
hist_base = hist_base/max(hist_base)
hist_test0 = cv.calcHist([gray_test0], [0], None, histSize, ranges)
hist_test0 = hist_test0/max(hist_test0)
hist_test1 = cv.calcHist([gray_test1], [0], None, histSize, ranges)
hist_test1 = hist_test1/max(hist_test1)
hist_test2 = cv.calcHist([gray_test2], [0], None, histSize, ranges)
hist_test2= hist_test2/max(hist_test2)
hist_test3 = cv.calcHist([gray_test3], [0], None, histSize, ranges)
hist_test3 = hist_test3/max(hist_test3)

# plt.plot(hist_base)
# plt.plot(hist_test0)
# plt.plot(hist_test1)
# plt.plot(hist_test2)
# plt.plot(hist_test3)
# plt.xlim([0,256])
# plt.show()

# plt.imshow(gray_test3)
# plt.show()

def dh_corr(h1, h2):
    mean_h1 = np.mean(h1)
    mean_h2 = np.mean(h2)
    temp1 = np.sum((h1 - mean_h1) * (h2 - mean_h2)) 
    temp2 = np.sqrt(np.sum((h1 - mean_h1)**2)*np.sum((h2 - mean_h2)**2))
    return temp1 / temp2

def dh_chi(h1, h2):
    return sum((t1 - t2)*(t1 - t2) / t1 for t1, t2 in zip(h1, h2))

def dh_inter(h1, h2):
    return sum(min(t1, t2) for t1, t2 in zip(h1, h2))

def dh_bha(h1, h2):
    return np.sqrt(1-1/np.sqrt(np.average(h1)*np.average(h2)\
        *len(h1)*len(h1))*sum(np.sqrt(t1 * t2) for t1, t2 in zip (h1, h2)))

def dh_cosine(h1, h2):
    # cosine similarity, there's a wheel existing with scipy
    def dot(h1, h2):
        return sum(a * b for a, b in zip(h1, h2))
    return dot(h1, h2)/(np.sqrt(dot(h1, h1))*np.sqrt(dot(h2, h2)))

def dh_hist(h1, h2):
    return sum(abs(t1-t2)/max(t1,t2) for t1, t2 in zip(h1, h2))/len(h1)

def compare_hist(h1, h2, method):
    return method(h1, h2)

methods = {'Correlation':dh_corr,'Chi-square':dh_chi,\
           'Intersection':dh_inter,'Bhattacharyya':dh_bha,\
           'Cosine':dh_cosine,'Hist Similarity':dh_hist}
for method,func in methods.items():
    base_base = func(hist_base, hist_base)
    base_test0 = func(hist_base, hist_test0)
    base_test1 = func(hist_base, hist_test1)
    base_test2 = func(hist_base, hist_test2)
    base_test3 = func(hist_base, hist_test3)
    print('Method: {} \n base_base, base_swap, test1_like, test2_unlike , base_half\n {} {} {} {} {}\n'\
          .format(method,base_base,base_test0,base_test1,base_test2,base_test3))
```

Expected outcomes:

We have OpenCV version as well:

```python
# histogram similarity calculation
# with rgb to hsv formats
# with opencv similarity calculation functions

import cv2 as cv
import numpy as np

src_base = cv.imread("dataset/base.jpg")
src_test0 = cv.imread("dataset/base_swap.jpg")
src_test1 = cv.imread("dataset/test1.jpg")
src_test2 = cv.imread("dataset/test2.jpg")

hsv_base = cv.cvtColor(src_base, cv.COLOR_BGR2HSV)
hsv_test0 = cv.cvtColor(src_test0, cv.COLOR_BGR2HSV)
hsv_test1 = cv.cvtColor(src_test1, cv.COLOR_BGR2HSV)
hsv_test2 = cv.cvtColor(src_test2, cv.COLOR_BGR2HSV)
hsv_half_down = hsv_base[hsv_base.shape[0]//2:,:]
h_bins = 50
s_bins = 60
histSize = [h_bins, s_bins]
# hue varies from 0 to 179, saturation from 0 to 255
h_ranges = [0, 180]
s_ranges = [0, 256]
ranges = h_ranges + s_ranges # concat lists
# Use the 0-th and 1-st channels
channels = [0, 1]
hist_base = cv.calcHist([hsv_base], channels, None, histSize, ranges, accumulate=False)
cv.normalize(hist_base, hist_base, alpha=0, beta=1, norm_type=cv.NORM_MINMAX)
hist_half_down = cv.calcHist([hsv_half_down], channels, None, histSize, ranges, accumulate=False)
cv.normalize(hist_half_down, hist_half_down, alpha=0, beta=1, norm_type=cv.NORM_MINMAX)
hist_test1 = cv.calcHist([hsv_test1], channels, None, histSize, ranges, accumulate=False)
cv.normalize(hist_test1, hist_test1, alpha=0, beta=1, norm_type=cv.NORM_MINMAX)
hist_test2 = cv.calcHist([hsv_test2], channels, None, histSize, ranges, accumulate=False)
cv.normalize(hist_test2, hist_test2, alpha=0, beta=1, norm_type=cv.NORM_MINMAX)
hist_test0 = cv.calcHist([hsv_test0], channels, None, histSize, ranges, accumulate=False)
cv.normalize(hist_test0, hist_test0, alpha=0, beta=1, norm_type=cv.NORM_MINMAX)

methods = ['Correlation','Chi-square',\
           'Intersection','Bhattacharyya']
for compare_method in range(4):
    method = methods[compare_method]
    base_base = cv.compareHist(hist_base, hist_base, compare_method)
    base_half = cv.(hist_base, hist_half_down, compare_method)
    base_test1 = cv.compareHist(hist_base, hist_test1, compare_method)
    base_test2 = cv.compareHist(hist_base, hist_test2, compare_method)
    base_test0 = cv.compareHist(hist_base, hist_test0, compare_method)
    print('Method:', method, '\nPerfect, base_swap, Base-Test(1), Base-Test(2) , Base-Half:\n',\
          base_base, '/', base_test0, '/', base_test1, '/', base_test2, '/', base_half,'\n')
```

[post status: half done]