+++
title = 'Principal Component Analysis (PCA)'
date = 2024-09-23T09:28:44-07:00
draft = true
+++

---

Let $X$ be an $n \times d$ matrix. In an experimental content, $X$ could be a data matrix with $n$ observations and $d$ features. If $d > 3$, we cannot visualize the data to observe patterns and structure. This is a problem because data visualization can yield significant insights into data. 

One solution is to reduce the dimensionality of the data. In other words, we can transform the $n \times d$ data matrix $X$ into an $n \times k$ data matrix $P$ where $k \leq 3$. To do so, we have to find a $d \times k$ transformation matrix $Z$ such that:

$$
P_{(n \times k)} = X_{(n \times d)}Z_{(d \times k)}
$$

In dimensionality reduction, there can be a loss of information. We want to minimize this as much as possible. Intuitively, the given data $X$ is "informative" if it exhibits high variance. So, to minimize the loss of information, we would like to **analyze** the data for key (**prinicipal**) **components** -- namely components that capture the maximal variance in the data.

How do we do this practically? There are two approaches. One uses the [Covariance Matrix]({{< ref "posts/covariance_matrix">}} "Covariance Matrix") of the data, while the other uses what is known as the [Singular Value Decomposition (SVD)]({{< ref "posts/svd">}} "SVD").








