Week 6 Lecture
========================================================

## Week 6 Readings

For this week, I suggest reading Aho Sections 6.5. In class this week, we will also discuss [Bender and Lange (2001)](https://github.com/hlynch/Biometry2023/tree/master/_data/Bender_Lange_2001.pdf), [Berger and Berry (1988)](https://github.com/hlynch/Biometry2023/tree/master/_data/Berger_Berry_1988.pdf), [Cohen (1994)](https://github.com/hlynch/Biometry2023/tree/master/_data/Cohen_1994.pdf), [Gawande (1999)](https://github.com/hlynch/Biometry2023/tree/master/_data/Gawande_1999.pdf), [Johnson (1999)](https://github.com/hlynch/Biometry2023/tree/master/_data/Johnson_1999.pdf), and [Nuzzo (2014)](https://github.com/hlynch/Biometry2023/tree/master/_data/Nuzzo_2014.pdf). Yes, there are a lot of papers this week, but I would encourage you to read efficiently - get the gist but don't get bogged down in the details. There is an overarching theme among these papers I want to make sure you really take to heart.

There are additional readings that I highlight here because they may be of interest, or may provide additional perspectives on the themes of the week, including [this paper on the problems of null hypothesis testing](https://github.com/hlynch/Biometry2023/tree/master/_data/Anderson_etal_2000.pdf), [this cheeky analysis of disease and astrological sign](https://github.com/hlynch/Biometry2023/tree/master/_data/Austin_etal_2006.pdf), [this paper on the hazards of sequential Bonferroni](https://github.com/hlynch/Biometry2023/tree/master/_data/Moran_2003.pdf), and [this review of the past, present, and future of null hypothesis testing](https://github.com/hlynch/Biometry2023/tree/master/_data/Robinson_Wainer_2002.pdf).

## Family-wise error rates

The ''family-wise error rate'' is

$$
\alpha = 1-(1-\alpha^{’})^k
$$

where $\alpha^{'}$ is the ''per-comparison error rate''. This is an important formula, don’t just memorize it - make sure you understand it!

Solution #1: One solution is to narrow down the model a priori to a single model that you think best captures the relevant biology of the system. 

Solution #2: Another work-around is to lower the threshold for significance so that the Type I error rate for the whole family of comparisons is still 5$\%$. There are several ways to do this, of which we will discuss two:

Method #1: The first method simply involves rearranging the formula above

$$
\alpha=1-(1-\alpha^{'})^{k}
$$
$$
\alpha^{'}=1-(1-\alpha)^{1/k}
$$

This method, called the Dunn-Šidák method, simply sets the per comparison error rate as above. This assumes that all the comparisons are independent.

Method #2: If the comparisons are not independent, then it is better to use a more conservative method, called Bonferroni’s method (of the Bonferroni correction)

$$
\alpha^{'}=\alpha⁄k
$$

However, this can set the per-comparison Type I error rate so low that it severely inflates the probability of a Type II error.

Solution #3: Sequential Bonferroni’s test – 

Let’s say you start with 10 comparisons. You would test each comparison, rank them in order of their p-values, and discard the least significant (highest p value) if it was not significant at the $\alpha$/10 level, the next least significant if it was not significant at the $\alpha$/9 level, and so forth until all remaining comparisons were significant using a Bonferroni adjusted critical value for the number of remaining comparisons.

Solution #4: Resampling-based corrected p-values – 

$$
P_{corrected} = P(min(p) \leq p-observed|H_{0})
$$

In other words, if you were to simulate data under the null hypothesis, what is the probability that the smallest p-value among the set of comparisons made is smaller than or equal to the p-value that you actually obtained. (In other words, the adjusted p-value asks “how extreme is my most extreme p-value when compared against the most extreme p-values I would expect under the null hypothesis?)


## How do we sort the signal from the noise?

One of the challenges we address this week is that almost all research programs involve multiple scientific hypotheses or exploratory analyses that are sifting through myriad potential causal drivers for observed phenomena. As a result, by the very structure of null hypothesis significance testing, we end up with a large number of false positive results from which it is often difficult to identify the ones most likely to represent real causal relationships. Though post-hoc studies can establish correlations, we know that correlation does not equal causation, and in fact only careful designed experiments can really confidently establish a causal relationship between a given variable and some observed response.

That said, there are clues that we can use to help us identify what is likely to be "real" amidst a sea of significant p-values. In 1965, Sir Austin Bradford Hill established a series of criteria in the Proceedings of the Royal Society of Medicine now known as the Bradford Hill criteria (Hill 1965). These criteria are summarized as follows (the attendant commentary is my own and may not hew exactly to Hill's original argument, which was focused on medical applications):

**Strength** or **Effect Size**: Covariates that have a larger effect on responses are more likely to have a causal relationship.

**Consistency**: Results that are reproducible by other researchers are more likely to be causal, and this is particularly true for results that can be reproduced in different systems and in different locations. (In other words, reproducible in this context also contains the idea of "extensibility".)

**Specificity**: Relationships that are very specific to a system in which no other plausible explanations exist are more likely to be causal.

**Temporality**: The response has to occur after the purported causal driver, and the time scale of the response has to make biological sense. 

**Biological gradient**: This captures the idea that causal drivers are usually dose-dependent, so greater exposure to the driver should result in a greater response.

**Plausibility**: There needs to be some plausible mechanism by which the driver could yield the response, though it may be that the exact mechanism involved in unknown.

**Coherence**: Findings in the field that more closely align with findings from controlled experiments are more likely to be causal.

**Analogy**: Proposed causal relationships are more likely to be causal if there are well-established analogs of similar relationships.

One of the applications in which correlation and causation is particularly difficult to establish is in the investigation of possible cancer clusters. Applying Hill's criteria to this application, we have to ask ourselves whether the hypothesized cancer causing agent 1) creates an increase in cancer incidence that is large enough to be biologically meaningful, 2) also causes an increase in cancers in other scenarios, 3) is specific to the population affected and the cancers involved have other causes, 4) the population was exposed to this hypothesized agent before the cancers were detected and that the time scale between exposure and the development of cancers is biologically reasonable, 5) people with greater exposure to the agent should have a greater risk than those with less exposure, 6) there is come mechanism by which the agent could possibly cause the cancer, 7) whether there is any experimental or laboratory findings to support the proposed mechanism, and 8) whether there are any other similar cancers that are caused by similar agents.
