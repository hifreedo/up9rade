---
layout: post
title: Convolution in forward and backward
---

# Convolution in forward and backward

Convolution neural network is a specific type of MLP, multi-layer perceptron, yet it complies with MLP's core, which is:
$$ y = w*x + b $$

With x been transferred forward, to get a cost function (which is a scalar) of:

$$ J(\theta, x, y) $$
We then back propagate the J, with gradient descent methodology, to compute:
$$ \frac{\partial J(\theta, x, y)}{\partial \theta} $$

Once done optimization with cost function J, which means we could get the representation parameters with given training data x and label data y.

Following is a simplified convolution network, let's assume an image input with 1 channel, a kernel filter with 1 channel and an output with padding on input layer, which makes the output size is same as input.

<img src="{{site.url}}/img/nn027.png">



$$ x = \begin{bmatrix}
x_1, x_2, x_3
\end{bmatrix}
\quad
w = \begin{bmatrix}
w_1 \\ w_2 \\ w_3
\end{bmatrix}
\\
y = xw = x_1w_1 + x_2w_2 + x_3w_3
\\
\frac{\partial y}{\partial w} = \begin{bmatrix}
\frac{\partial y}{\partial w_1} \\ \frac{\partial y}{\partial w_2} \\ \frac{\partial y}{\partial w_3}
\end{bmatrix} = \begin{bmatrix}
x_1 \\ x_2 \\ x_3
\end{bmatrix}
= x^T
$$

$$

A = \begin{bmatrix}
a_1 & a_2 \\ a_3 & a_4
\end{bmatrix}
\qquad
B = \begin{bmatrix}
b_1 & b_2 \\ b_3 & b_4
\end{bmatrix}
\qquad
C = \begin{bmatrix}
c_1 & c_2 \\ c_3 & c_4
\end{bmatrix}
\\
\\
C = AB
\\
\begin{cases}
c_1 = a_1b_1 + a_2b_3 \\
c_2 = a_1b_2 + a_2b_4 \\
c_3 = a_3b_1 + a_4b_3 \\
c_4 = a_3b_2 + a_4b_4
\end{cases}
\\
\frac{\partial C}{\partial A} = \begin{cases}
\frac{\partial c_1}{\partial a_1} = b_1 \\
\frac{\partial c_1}{\partial a_2} = b_3 \\
\frac{\partial c_1}{\partial a_3} = 0 \\
\frac{\partial c_1}{\partial a_4} = 0 \\
\frac{\partial c_2}{\partial a_1} = b_2 \\
\frac{\partial c_2}{\partial a_2} = b_4 \\
...
\end{cases}

$$

