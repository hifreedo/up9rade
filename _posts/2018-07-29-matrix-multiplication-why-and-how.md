---
layout: post
title: Matrix Multiplication
---

# Matrix multiplication why and how

## Why matrix and its multiplication is so important in neural network

## How to code multiplication

Matrix multiplication in processing:

```processing

Matrix multiply(Matrix a, Matrix b) {
  // matual product
  if (a.cols != b.rows) {
    return null;
  }
  Matrix result = new Matrix(a.rows, b.cols);
  for (int i = 0; i < a.rows; i++) {
    for (int j = 0; j < b.cols; j++) {
      float sum = 0;
      for (int k = 0; k < a.cols; k++) {
        sum += a.data[i][k] * b.data[k][j];
      }
      result.data[i][j] = sum;
    }
  }
  return result;
}

```

## How to code in a more efficient way for multiplication

[post status: needs to be implemented]