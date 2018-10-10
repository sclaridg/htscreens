# CRISPR Analysis

Analysis of the Broad's Avana CRISPR (Broad Institute Cancer Dependency Map 2018, Meyers et al. 2017).

The Avana screen produced results using [CERES](https://depmap.org/ceres/) (Meyers et al. 2017) ([GitHub](https://github.com/cancerdatasci/ceres)), which generates gene dependency scores from sgRNA depletion scores from gene essentiality screens and eliminates bias arising from the effect of copy number variation on Cas9 DNA cleavage. The lower the CERES score, the higher the likelihood that the gene is essential in the associated cell line. Scores are scaled per cell line such that a score of 0 is the median effect of nonessential genes and -1 is the median effect of common core essential genes.

All annotation files (copy number, mutation status, and gene expression) (Consortium and Consortium 2015, Barretina et al. 2012) were downloaded from the [DepMap Data Portal](https://depmap.org/portal/download/). G2P data was scraped from the [G2P database](search.cancervariants.org) by Daniel Charytonowicz.

## Contents

- **`data_munging`**: [Cancer Cell Line Encyclopedia (CCLE)](https://portals.broadinstitute.org/ccle) genomic annotations, CRISPR screen metadata, rds data files produced in the Rmd, and versioned G2P datasets
- **`plots_18Q3`**: Plots created in the Rmd
- **`lineages_18Q3.Rmd`/`html`**: Code to use and generate files in `data_munging` and figures in `plots`

## References

Barretina, J., Caponigro, G., Stransky, N., Venkatesan, K., Margolin, A. A., Kim, S., … Garraway, L. A. (2012). The Cancer Cell Line Encyclopedia enables predictive modelling of anticancer drug sensitivity. Nature, 483(7391), 603–607. https://doi.org/10.1038/nature11003

Broad Institute Cancer Dependency Map; Cancer Data Science (2018): Cancer Dependency Map, CRISPR Avana dataset 18Q3 (Avana_public_18Q3). figshare. Fileset. doi:10.6084/m9.figshare.6931364.v1

Consortium, T. C. C. L. E., & Consortium, T. G. of D. S. in C. (2015). Pharmacogenomic agreement between two cancer cell line data sets. Nature, 528(7580), 84–87. https://doi.org/10.1038/nature15736

Doench, J. G., Fusi, N., Sullender, M., Hegde, M., Vaimberg, E. W., Donovan, K. F., … Root, D. E. (2016). Optimized sgRNA design to maximize activity and minimize off-target effects of CRISPR-Cas9. Nature Biotechnology, 34(2), 184–191. https://doi.org/10.1038/nbt.3437

Meyers, R. M., Bryan, J. G., McFarland, J. M., Weir, B. A., Sizemore, A. E., Xu, H., … Tsherniak, A. (2017). Computational correction of copy-number effect improves specificity of CRISPR-Cas9 essentiality screens in cancer cells. Nature Genetics, 49(12), 1779–1784. https://doi.org/10.1038/ng.3984