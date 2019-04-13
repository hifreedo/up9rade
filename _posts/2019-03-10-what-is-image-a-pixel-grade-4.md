---
layout: post
title: What is image file [grade 4]
---

# What is image file: behind a pixel

## grade 4: behind a pixel

Let's try to dig what's behind an image from a popular website, i.e. amazon, facebook.

Right click the mouse, choose open image in new tab, and you will see a long url like the following:
[https://images-na.ssl-images-amazon.com/images/..._260x260_1550730012_jpg](https://images-na.ssl-images-amazon.com/images/G/01/US-hq/2019/img/Certified_Refurbished/XCM_Manual_1161174_renewed_card_resize_260x260_Certified_Refurbished_XCM_Manual_1161174_us_certified_refurbished_renewed_card_resize_260x260_1550730012_jpg._CB454883446_SY260_.jpg)

First of all, the image comes with a height & width in pixels, for e.g. we see 260x260 from amazon.

What's the actual file size aka how much disk space will it take to save a 260x260 pixels image? 

Image size = 260 x 260 * 3 bytes / 1024 kb = 198 kb

A little bit explanation on the equation:

Normally images of jpg on the web, they were consists of 3 color channels, the RGB "red, green, blue". 
For each channel, use a number in between 0 to 255 to denote, to do so, which takes 8 bits, each bit represents 0 or 1.

Hence, 1 pixel from an image, could use 3 bytes to denote its 3 color channels. 

1 Kb = 1024 bytes.

This is the same size if you open this image in photoshop.
But wait, if you check the image file info in your operation system, doesn't matter Mac or Wins, you found it's not the number of 198 kb as we calculated on the "size". 

What's going on? 

In image compression, the file size is not calculated by its pixels. As we introduced in previous post,  [What is image file]({{site.url}}/2018/08/26/what-is-image-jpeg-heif-grade-1.html), jpeg is the commonly used lossy compression for images.


