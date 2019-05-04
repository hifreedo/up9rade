---
layout: post
title: PCA and related
---

# PCA and related

Principal component analysis is a methodology widely implemented in dimensionality reduction.

PCA relies on orthogonal transformation, to covert a set of possibly correlated variables into a set of linearly independent / uncorrelated variables, which were called principal components.

Though tends to minimize information loss, it's a "lossy compression". 

|     | PCA  | SVD
|  ----  | ----  | ----
| purpose  | dimensionality reduction | matrix decomposition
| sparse data  | not support, zero mean data | supports sparse matrix
| computation | less efficient, needs solve cov matrix  | efficient
| reduction | one way, dimensionality | bilateral, dimensionality(right matrix) and sample numbers(left matrix)


