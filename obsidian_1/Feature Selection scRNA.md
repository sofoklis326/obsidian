
Heterogeneity across cells
gene abundance, gene level of expression
bulk RNA or scRNA datasets
Gene expression counts across cells -> log
Suppose that variance represents noise of the counting
we split the variance in the technical (noise) and biological variance.

plot log mean vs log variance for each gene, and fit a line through the scatter plot.
Increased expression levels = higher or constant technical variance, lower biological variance
The slope of the line represents the coefficient of variation (CV) bet
between biological and technical variances.
we can also fit a line only to the spike in transcripts to not let upregulated genes inflate the fitted line

Select highly variable genes (HVG)
A larger subset will reduce the risk of discarding interesting biological signal by retaining more potentially relevant genes, at the cost of increasing noise from irrelevant genes that might obscure said signal. It is difficult to determine the optimal trade-off for any given application as noise in one context may be useful signal in another.

 heterogeneity in T cell activation responses is an interesting phenomena (Richard et al. [2018](https://bioconductor.org/books/3.13/OSCA.basic/feature-selection.html#ref-richard2018tcell)) but may be irrelevant noise in studies that only care about distinguishing the major immunophenotypes.

