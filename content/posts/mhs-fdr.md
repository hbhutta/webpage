+++
title = 'Multiple Hypothesis Testing and the False Discovery Rate'
date = 2024-09-24T10:52:21-07:00
draft = true
+++

---
# Background and motivation
## Hypothesis Testing
A *hypothesis* is a guess. In any (statistical) hypothesis test, we have a null hypothesis ($H_{0}$) and an *alternative* hypothesis ($H_{a}$). The latter is named as such because it is the *alternative* guess, opposite of $H_{0}$. We decide to accept or reject $H_{0}$ based on a quantity called the [${p}$-value](#p-value), derived from the **test statistic** which itself is obtained from the **statistical test** we choose to use considering our data.

## $p$-value and the significance level $\alpha$
The $p$-value is the likelihood of falsely rejecting the null hypothesis $H_{0}$. It was decided by [Ronald Fisher](https://en.wikipedia.org/wiki/Ronald_Fisher)[^1] that having $p < 0.05$ means there is less than a $5\\%$ chance of falsely rejecting $H_0$ so it is safe to do so, and having $p > 0.05$ means there is more than a $5\\%$ chance of falsely rejecting $H_{0}$ so it is *not* safe to do so. In other words, $5\\%$ is the threshold for determining if the likelihood of falsely rejecting $H_{0}$ is trivial or non-trivial.

I do not prefer the phrasing that "the smaller the $p$-value, the stronger the evidence against $H_{0}$" as it is sometimes described in courses, especially with the use of the word "evidence", since the $p$-value is not a measure of certainty but a measure of likelihood.



The significance level $\alpha$ is the likelihood of falsely rejecting the $H_{0}$ which I, as the experimental investigator, decide on. This $\alpha$ is the threshold we use in determining if the likelihood of rejecting $H_{0}$ that we have obtained is trivial or non-trivial.

## Type I (T1) and Type II (T2) Error
An error is a mistake. T1 and T2 errors are mistakes. In clinical trials, sometimes we accidentally make mistakes. It's important to know the proportion of our claims that are mistakes, and to minimize this proportion -- if not completely eliminate it.

A T1 error occurs when we falsely reject $H_{0}$:
- It is a *false acceptance* of the altnernative hypothesis $H_{a}$ -- hence **a T1 error is a false positive**

A T2 error occurs when 
- It is a *false rejection* of the 




For example, suppose we are conducting an RNA-seq experiment with the following null and alternative hypotheses:
$$
\begin{cases}
    H_{0}: \text{The mean gene expression of gene $g$ is the same in treatments $T_{1}$ and $T_{2}$} \\\
    H_{a}: \text{The mean gene expression of gene $g$ is different in treatments $T_{1}$ and $T_{2}$}
\end{cases}
$$
In this example, a false positive (T1 error) would be accepting (affirming) $H_{a}$ when $H_{0}$ is (very likely to be) true
(as indicated by the $p$-value), and a false negative (T2 error) would be rejecting (not affirming) $H_{a}$ when


Bonferroni error rate correction (type 1 error rate control)




## Mutliple Hypothesis Testing and the Multiple Comparisons Problem 
In differential gene expression analysis, we want to know if a given gene $g$ has different mean expression levels in different treatments (groups). Comparing means makes this a statistical question. Supposing we have gene $g$ and treatments $T_{1}, \ldots, T_{k}$, and supposing that the mean expression level (however this is measured) of gene $g$ in treatment $T_{i}$ is denoted as $\mu_{g, T_{i}}$, we have the following null and alternative hypotheses *for each gene* $g$:
$$
\begin{cases}
    H_{0}: \forall 1 \leq i \neq j \leq k, \mu_{g, T_{i}}  =    \mu_{g, T_{j}} \\\
    H_{a}: \exists i,j \in [1, \ldots, k]: \mu_{g, T_{i}}  \neq \mu_{g, T_{j}}
\end{cases}
$$
In the null hypothesis $H_{0}$, we hypothesize that any two treatments $T_{i}$ and $T_{j}$ have the same mean expression level of gene $g$. In the alternative hypothesis $H_{a}$, we hypothesize that there exist at least two treatments $T_{i}$ and $T_{j}$ with *different* mean expression levels of gene $g$.

We will have this set of hypotheses *for each gene*, hence the situation becomes *multiple hypothesis testing*.

## False discovery rate

Recall that the $p$-value is the likelihood of falsely rejecting $H_{0}$. When we reject $H_{0}$ we accept the alternative, $H_{a}$. Typically in science (e.g. in clinicial trials of a drug), $H_{0}$ is what the scientists "expect" with their domain knowledge. But they formulate $H_{0}$ and $H_{a}$ anyway because there is the possibility for the data to indicate what they may not expect; the data may indicate $p < \alpha$ making it safe to reject $H_{0}$ and accept $H_{a}$ -- **a new discovery**. 

However, there is the chance of falsely rejecting $H_{0}$ (i.e. accepting $H_{a}$) (i.e. making a *false discovery*). Ideally, we want the rate of this false discovery -- literally the *"false discovery rate" (FDR)*  -- to be at a minimium, for obvious reasons.

Now, we know that if $p < 0.05$ we can reject $H_{0}$ and accept $H_{0}$ and "make a discovery". But suppose, for the sake of argument, that this is a false discovery.

## Family-wise error rate 

The *family-wise error rate* (FWER) is a measurement of Type I error likelihood when making multiple comparisons. For $k$ independent hypothesis tests, each with a significance level $\alpha$, the upper on the FWER is:
$$
\text{FWER} \leq 1 - (1 - \alpha)^{k}
$$

For example, suppose we have $\alpha = 0.05$ for a hundred independent tests (e.g. for a hundred different genes in differential gene expression analysis). Below we show the FWER for just one test, compared to a hundred independent tests:
$$
\begin{cases}
    \text{\# tests = 1}: \text{FWER} = 1 - (1 - 0.05)^{1} = 0.05 = 5\\% \\\
    \text{\# tests = 2}: \text{FWER} = 1 - (1 - 0.05)^{2} = 0.0975 = 9.75\\% \\\
    \text{\# tests = 3}: \text{FWER} = 1 - (1 - 0.05)^{3} = 0.142625 = 14.26\\% \\\
    ... \\\
    \text{\# tests = ...}: \text{FWER} = 1 - (1 - 0.05)^{100} \approx 0.99407 \approx 99.41\\% \\\
\end{cases}
$$

## Bonferroni correction

Knowing that we only make a "discovery" in a particulra hypothesis test when $p < \alpha$, the if the significance threshold $\alpha$ were lower, wouldn't we be rejecting $H_{0}$ less often, and, in other words, be making fewer discoveries? And if we were making fewer discoveries, wouldn't we also be making fewer *false* discoveries? This is the idea behind *Bonferroni correction*. 

When conducting $k$ hypothesis tests, with significance level $\alpha$, define the new significance level $\alpha'$ as:
$$
\alpha' = \frac{\alpha}{k}
$$

Now, for each of the hypothesis tests in the multiple hypothesis testing, reject $H_{0}$ if $p < \alpha'$, not if $p < \alpha$.

As the whole idea of Bonferroni correction is to reduce the chance of making false discoveries by reducing the chance of making any discoveries at all, one obvious problem with it is that we also reduce the chance of making any true discoveries. In other words, Bonferroni correction reduces the [statistical power]() of our study.


An alternative to Bonferroni correction is the *Benjamini-Hochberg procedure* for controlling the FDR. 

## Benjamini-Hochberg procedure


[^1]: The intersted reader can refer to [this Reddit explanation](https://www.reddit.com/r/askscience/comments/vxink/why_is_p005_the_magic_number_for_significance/) of why Fisher chose $0.05$ as his significance threshold
[^2]: Higdon, R. (2013). Multiple Hypothesis Testing. In: Dubitzky, W., Wolkenhauer, O., Cho, KH., Yokota, H. (eds) Encyclopedia of Systems Biology. Springer, New York, NY. https://doi.org/10.1007/978-1-4419-9863-7_1211
[^3]: Haynes, W. (2013). Benjamini–Hochberg Method. In: Dubitzky, W., Wolkenhauer, O., Cho, KH., Yokota, H. (eds) Encyclopedia of Systems Biology. Springer, New York, NY. https://doi.org/10.1007/978-1-4419-9863-7_1215
[^4]: https://www.sciencedirect.com/science/article/abs/pii/B9780080448947015621
