+++
title = 'Multiple Hypothesis Testing and the False Discovery Rate'
date = 2024-09-24T10:52:21-07:00
draft = true
+++

---
# Background and motivation

## Hypothesis Testing
A *hypothesis* is a guess. In any (statistical) hypothesis test, we have a null hypothesis ($H_{0}$) and an *alternative* hypothesis ($H_{a}$). The latter is named as such because it is the *alternative* guess, opposite of $H_{0}$. We decide to accept or reject $H_{0}$ based on a quantity called the [${p}$-value](#p-value), derived from the **test statistic** which itself is obtained from the **statistical test** we choose to use considering our data.

## $p$-value
The $p$-value is the likelihood of falsely rejecting the null hypothesis $H_{0}$. It was arbitrarily decided by [Ronald Fisher](https://en.wikipedia.org/wiki/Ronald_Fisher) that having $p < 0.05$ means there is less than a $5\\%$ chance of falsely rejecting $H_0$ so it is safe to do so, and having $p > 0.05$ means there is more than a $5\\%$ chance of falsely rejecting $H_{0}$ so it is *not* safe to do so. In other words, $5\\%$ is the threshold for determining if the likelihood of falsely rejecting $H_{0}$ is trivial or non-trivial. 

### How the $p$-value accounts for intra-group variability
Intuitively, drawing a conclusion from comparing the means of groups with *large* intra-group variability would not be as "significant" as drawing the same conclusion from a comparison of groups with *low* intra-group variability.


For example, there are infinitely many pairs $(x,y)$ that satisfy the below equation:
$$
\frac{x+y}{2} = 1
$$

In other words, there are infinitely many points $(x,y)$ whose mean is 1. For example $(x,y) = (2,0)$ and $(x,y) = (1,1)$ satisfy this equation. But $|2-0| \neq |1-1|$; meaning if $x$ and $y$ are individual data points in a dataset whose mean we are taking, then the "group" $(x,y) = (2,0)$ has more intra-group variability than the group $(x,y) = (1,1)$

## Mutliple Hypothesis Testing and the Multiple Comparisons Problem 

In differential gene expression analysis, we want to know if a given gene $g$ has different mean expression levels in different treatments (groups). Comparing means makes this a statistical question. Supposing we have gene $g$ and treatments $T_{1}, \ldots, T_{k}$, and supposing that the mean expression level (however this is measured) of gene $g$ in treatment $T_{i}$ is denoted as $\mu_{g, T_{i}}$, we have the following null and alternative hypotheses *for each gene* $g$:
$$
\begin{cases}
    H_{0}: \forall 1 \leq i \neq j \leq k, \mu_{g, T_{i}}  =    \mu_{g, T_{j}} \\\
    H_{a}: \exists i,j \in [1, \ldots, k]: \mu_{g, T_{i}}  \neq \mu_{g, T_{j}}
\end{cases}
$$

We will have this set of hypotheses *for each gene*, hence the situation becomes *multiple hypothesis testing*.

In the null hypothesis $H_{0}$, we hypothesize that any two treatments $T_{i}$ and $T_{j}$ have the same mean expression level of gene $g$. In the alternative hypothesis $H_{a}$, we hypothesize that there exist at least two treatments $T_{i}$ and $T_{j}$ with *different* mean expression levels of gene $g$.






~~Since there are $k$ means (i.e. each treatment (group) $T_{i}$ notes a mean expression level for gene $g$), and we do not assume normality of the data, we have to use a non-parametric statistical test to compare the $k$ means. Namely, we use the *Kruskal-Wallis* test.~~




[^1]: Higdon, R. (2013). Multiple Hypothesis Testing. In: Dubitzky, W., Wolkenhauer, O., Cho, KH., Yokota, H. (eds) Encyclopedia of Systems Biology. Springer, New York, NY. https://doi.org/10.1007/978-1-4419-9863-7_1211
[^2]: Haynes, W. (2013). Benjamini–Hochberg Method. In: Dubitzky, W., Wolkenhauer, O., Cho, KH., Yokota, H. (eds) Encyclopedia of Systems Biology. Springer, New York, NY. https://doi.org/10.1007/978-1-4419-9863-7_1215
