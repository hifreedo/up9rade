---
layout: post
title: Matrix Multiplication
---

# Matrix multiplication why and how

## Why matrix and its multiplication is so important in neural network

## How to code multiplication

In the previous post of [xor problem]({{site.url}}/2018/06/19/neural-network-xor-problem-grade-3.html), we introduce the network of 2 inputs nodes, 2 hidden nodes and 1 output as the following:

<img src="{{site.url}}/img/nn019.png">

We calculate the values of P1 & P2 as following:

$$ \begin{cases}
  W_1 * L_1 + W_3 * L_2 = P_1 \\
  W_2 * L_1 + W_4 * L_2 = P_2
  \end{cases}$$

The linear functions is exact the format of matrix as following:

$$
\begin{pmatrix}
     W_1 & W_3 \\
     W_2 & W_4
\end{pmatrix}
*
\begin{pmatrix}
     L_1 \\
     L_2
\end{pmatrix}
=
\begin{pmatrix}
     P_1 \\
     P_2
\end{pmatrix}
$$

Every matrix represents some linear function, and every linear function is represented by a matrix. That's the strong connection between the linear function and matrix. In linear space, matrix multiplication represents linear transformation, i.e. a movement in space. The first matrix {w} means movement, the second matrix {L} is the basis, the third {P} is the new location.

So in linear space, the network represents through a set of transformation, the original input outputs the result we expect to, either classification problem or regression problem.

Matrix is a perfect tool for neural network computation.

<img src="{{site.url}}/img/nn020.png">

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