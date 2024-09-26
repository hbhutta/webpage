+++
title = 'Assessment of Variability'
date = 2024-09-24T15:49:42-07:00
draft = true
+++

---

In the data analysis of RNA-seq data, we want to assess the *inter-group variability* and the *intra-group variability*. *Inter-group variability* is the variability between different groups (a.k.a conditions, groups). For example, the differential expression of a gene between two groups is a type of inter-group variability. *Intra-group variability* is the variability *within* a group, amongst the samples in that group. Intra-group variability arise from the technical and biological differences in the sampling procedure for different samples[^1]. For example, two samples within a group could be taken on different days or stored in different temperature conditions -- this would be a technical difference between the two samples.

~~Assessing variability within the data is a form of quality assurance. Two useful techniques for identifying inter- and intra-group variability are [principal component analysis (PCA)]({{<ref "posts/pca">}} "Principal Component Analysis") and Pearson correlation heatmaps. The latter visualize correlation between samples (???)~~

Consider this small mathematical example. There are infinitely many pairs $(x,y)$ that satisfy the below equation:
$$
\frac{x+y}{2} = 1
$$

In other words, there are infinitely many points $(x,y)$ whose mean is 1. For example $(x,y) = (2,0)$ and $(x,y) = (1,1)$ satisfy this equation. But $|2-0| \neq |1-1|$; meaning if $x$ and $y$ are individual data points in a dataset whose mean we are taking, then the "group" $(x,y) = (2,0)$ has more intra-group variability than the group $(x,y) = (1,1)$


[^1]: Koch CM, Chiu SF, Akbarpour M, Bharat A, Ridge KM, Bartom ET, Winter DR. A Beginner's Guide to Analysis of RNA Sequencing Data. Am J Respir Cell Mol Biol. 2018 Aug;59(2):145-157. doi: 10.1165/rcmb.2017-0430TR. PMID: 29624415; PMCID: PMC6096346.





