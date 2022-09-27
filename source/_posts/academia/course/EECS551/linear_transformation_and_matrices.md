---
title: Linear transformations and matrices
categories:
- Academia
tags:
- LinearAlgebra
- 3blue1brown
---

# Linear transformations

Transformation is like function but it focusing on moving.

Linear
- lines remain lines
- origin remains fixed

> Grid lines remain paralled and evenly space

# How to think about transformation

Before transformation we need to record where the basis vectors land. `v` vector is `-1 * i + 2 * j`
![](https://i.imgur.com/rd8jCks.png)

After transformation we also need to record where the transformed basis vectors land. `v` vector is `-1 * i(transformed) + 2 * j(transformed)`
![](https://i.imgur.com/TYZDMm2.png)


# Matrices

Matrices can be thought of a set of transformed `i` and transformed `j` in columes.
![](https://i.imgur.com/UOpkZYG.png)

To calculate where the transformed vector lands, we just need to multiply x by first column plus multiply y by second column.
![](https://i.imgur.com/7Tshu6q.png)

Matrices is a way of package information needed to desctibe a linear transformation.
![](https://i.imgur.com/MYeXyz8.png)

This also shows why a matrix multiply a vector in this way, the first element is each elements in the first row multiply by corresponding each elements in the first column of the vector.


# Specific

The transformation of 90 degree rotation counterclockwise.
![](https://i.imgur.com/RCUIY5t.png)

The transformation of Shear
![](https://i.imgur.com/PegyJMj.png)

If the columns are linearly dependent, all the transformed vectors will be squeezed in to a line. 

- 2-D space is squeezed into a line
- the span of these two linearly dependent is 1-D


![](https://i.imgur.com/IS9bLmS.png)



----
Reference
https://www.3blue1brown.com/topics/linear-algebra