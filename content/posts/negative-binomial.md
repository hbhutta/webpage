+++
title = 'Negative Binomial Distribution'
date = 2024-09-24T16:57:02-07:00
draft = true
+++

---

With the NB distribution, we can ask, for example: 

> *"What is the probability of rolling the fifth 6 on the twentieth roll of a die?"*

This question suggests that:

1. The twentieth roll of the die *must* be one of the five 6's that must be rolled in order to get a "5th 6"
2. The other four 6's *must* have been rolled in the previous nineteen rolls

For the second, point, just like in the binomial distribution, we have to pick four rolls out of nineteen to be our "successes". There are ${19 \choose 4} = {20 - 1 \choose 5 - 1}$ ways to do this. If the "success" probability is $p$ then, by the product rule of probability, the probability of getting $4$ success is $p^{4}$. The remaining $(20-1)-(5-1) = 15$ trials must be failures then, the probability of getting this many failures -- again by the product rule of probability -- must be $(1-p)^{15}$. Altogether, if we want the $x$-th trial to be the $r$-th success, then out of the previous $x-1$ trials we must have had $r-1$ successes, meaning a total of $(x-1)-(r-1) = x - r$ failures. Therefore, if the random variable $X$ follows the NB distriibution, then:
$$
P(X=x) = { x - 1 \choose r - 1}(1-p)^{x-r}p^{r}
$$

We denote that "$X$ follows a NB distribution" if $X \sim \text{NB}(p)$, where $p$ is the probability of success.
