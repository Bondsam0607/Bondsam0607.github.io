---
layout: page
title: Linear Algebra
tags: Math
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image: false
excerpt_separator: <!--more-->
---

Linear Algebra is manipulations of vectors and matrices.

<!--more-->

## Linear combination, span, and basis vectors

### Linear combination

Linear combination of $$\vec{v}$$ and $$\vec{w}$$:

$$a\vec{v}+b\vec{w}$$

$$a,b$$ are scalars

### Linear dependent

if a vector $$\vec{u}$$ can be expressed by $$\vec{u}=a\vec{v}+b\vec{w}$$, it is called linear dependent.

### span

a n-dimension span is spanned up by n vectors which are not linear dependent to each other.

### basis vector

basis vectors are serveral vectors which are perpendicular to each other.

basis vectors are often used to describe other vectors in the span which is spanned up by the n basis vectors.

## Linear transformation and matrices

Actually matrices are linear transformation.

### What is a linear transformation?

if after a transformation, all the lines in the original span is still lines and the origin stay unchanged, the transformation is called linear transformation.

### What are matrices?

Matrices are manipulations of vector span.

From above, we can know that a span is basically described by basis vectors. 

So the effect of a matrix is just changing the basis vectors.

For example, a matrix $$
\begin{equation*}
A = 
\begin{bmatrix}
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9
\end{bmatrix}
\end{equation*}$$ is to change the basis vectors which are $$
\begin{equation*}
\begin{bmatrix}
1\\
0\\
0
\end{bmatrix}
\end{equation*}$$,$$
\begin{equation*}
\begin{bmatrix}
0\\
1\\
0
\end{bmatrix}
\end{equation*}$$,$$
\begin{equation*}
\begin{bmatrix}
0\\
0\\
1
\end{bmatrix}
\end{equation*}
$$ to $$
\begin{equation*}
\begin{bmatrix}
1\\
4\\
7
\end{bmatrix}
\end{equation*}$$,$$
\begin{equation*}
\begin{bmatrix}
2\\
5\\
8
\end{bmatrix}
\end{equation*}$$,$$
\begin{equation*}
\begin{bmatrix}
3\\
6\\
9
\end{bmatrix}
\end{equation*}
$$

$$
\begin{equation*}
\begin{bmatrix}
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9
\end{bmatrix}
\begin{bmatrix}
1\\
2\\
3
\end{bmatrix}
\end{equation*}
$$
changes from 
$$
\begin{equation*}
1*
\begin{bmatrix}
1\\
0\\
0
\end{bmatrix}
+2*
\begin{bmatrix}
0\\
1\\
0
\end{bmatrix}
+3*
\begin{bmatrix}
0\\
0\\
1
\end{bmatrix}
\end{equation*}
$$
to
$$
\begin{equation*}
1*
\begin{bmatrix}
1\\
4\\
7
\end{bmatrix}
+2*
\begin{bmatrix}
2\\
5\\
8
\end{bmatrix}
+3*
\begin{bmatrix}
3\\
6\\
9
\end{bmatrix}
\end{equation*}
$$

I think this is a complete explanation of matrices.

### The determinant

A determinant is a measure of the size/area of a matrix.

For example, the determinant of matrix 
$$
\begin{equation*}
\begin{bmatrix}
1 & 0\\
0 & 1
\end{bmatrix}
\end{equation*}
$$
is 1 which means that the area of this matrix is 1 which is the area made up of vectors
$$
\begin{equation*}
\begin{bmatrix}
1\\
0
\end{bmatrix}
and 
\begin{bmatrix}
0\\
1
\end{bmatrix}
\end{equation*}
$$

Then we multiply the matrix with 
$$
\begin{equation*}
\begin{bmatrix}
3 & 0\\
0 & 4
\end{bmatrix}
\end{equation*}
$$
and its determinant is 12 and is the area made up of vectors
$$
\begin{equation*}
\begin{bmatrix}
3\\
0
\end{bmatrix}
and 
\begin{bmatrix}
0\\
4
\end{bmatrix}
\end{equation*}
$$

Then we take a look at a special situation where the determinant of the matrix is 0.

If the determinant of a matrix is 0, it means that the matrix squeeze the vector spacve into a lower dimension space such as from a cube to a panel or from a panel to a line.

So it makes sense that the determinant is 0 because the area is zero.

## Inverse matrices, column space and null space

### Inverse matrices

if a matrix is the manipulation of the space, then the inverse matrix is just the inverse manipulation of the space.

### column space

