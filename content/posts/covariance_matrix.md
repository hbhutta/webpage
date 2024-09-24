+++
title = 'Covariance Matrix'
date = 2024-09-23T12:48:51-07:00
draft = true
+++

##### Definition:
Let $X \in \mathbb{R}^{n \times d}$. Refer to the $d$-th column (feature) of $X$ as $f_{d}$. The *covariance matrix* $\text{Cov}(X)$ is the following real, symmetric matrix:

$$
\text{Cov}(X) = 
\begin{bmatrix}
\text{Cov}(f_{1}, f_{1}) & \text{Cov}(f_{1}, f_{2}) & \ldots & \text{Cov}(f_{1}, f_{d}) \\\
\text{Cov}(f_{2}, f_{1}) & \text{Cov}(f_{2}, f_{2}) & \ldots & \text{Cov}(f_{2}, f_{d}) \\\
\vdots & \vdots & \ddots & \vdots \\\
\text{Cov}(f_{d}, f_{1}) & \text{Cov}(f_{d}, f_{2}) & \ldots & \text{Cov}(f_{d}, f_{d}) \\\
\end{bmatrix}
$$

On a related note, the covariance $\text{Cov}(X,Y)$ of two random variables $X$ and $Y$ is defined as:
$$
\text{Cov}(X,Y) = E((X-\mu_{X})(Y-\mu_{Y}))
$$
Which itself is a generalization of the *variance* of a random variable $X$:
$$
\text{Cov}(X,X) = E((X-\mu_{X})(X-\mu_{X})) = E((X-\mu_{X})^{2}) = \text{Var}(X)
$$

This means that if we *zero-mean* (i.e. "center") the data matrix $X$, such that $X := X - \mu_{X}$, then:
$$
\text{Cov}(X) = \frac{1}{n-1}X^{T}X
$$






