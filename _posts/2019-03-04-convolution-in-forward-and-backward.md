---
layout: post
title: Convolution in forward and backward
---

# Convolution in forward and backward

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

