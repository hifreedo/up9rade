---
layout: post
title: PCA and related
---

# PCA and related

Principal component analysis is a methodology widely implemented in dimensionality reduction.

PCA relies on orthogonal transformation, to covert a set of possibly correlated variables into a set of linearly independent / uncorrelated variables, which were called principal components.

The difference between PCA & linear regression, to the latter, the cost function is:

$$argmin\frac{1}{2}(h(\Theta)-y)^2$$

While the measurement for PCA is different. The optimization is to lead to:

* maximum variance (which remains maximum original data information)
* minimum covariance (which eliminates correlated dimensions)

Though tends to minimize information loss, it's a "lossy compression". 

Steps of calculating PCA:
1. Zero mean of dataset;
2. Covariance matrix;
3. Eigenvectors & eigenvalues;
4. Decide top K values;

|     | PCA  | SVD
|  ----  | ----  | ----
| purpose  | dimensionality reduction | matrix decomposition
| sparse data  | not support, zero mean data | supports sparse matrix
| computation | less efficient, needs solve cov matrix  | efficient
| reduction | one way, dimensionality | bilateral, dimensionality(right matrix) and sample numbers(left matrix)


Other than dimensionality reduction, PCA was introduced into image argumentation with the "ImageNet Classiﬁcation with Deep Convolutional Neural Network" aka AlexNet.

[post status: fresh start]