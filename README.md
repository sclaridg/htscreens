# CRISPR Lineage Analysis

Analysis of the Broad's Avana CRISPR (Broad Institute Cancer Dependency Map 2018, Meyers et al. 2017) and the Broad and Dana-Farber Cancer Institite's Achilles shRNA (MacFarland et al. 2018, Data Science 2018).

The Avana screen produced results using [CERES](https://depmap.org/ceres/) (Meyers et al. 2017) ([GitHub](https://github.com/cancerdatasci/ceres)), which generates gene dependency scores from sgRNA depletion scores from gene essentiality screens and eliminates bias arising from the effect of copy number variation on Cas9 DNA cleavage. The lower the CERES score, the higher the likelihood that the gene is essential in the associated cell line. Scores are scaled per cell line such that a score of 0 is the median effect of nonessential genes and -1 is the median effect of common core essential genes.

In a previous version of the shRNA screen, DEMETER ([GitHub](https://github.com/cancerdatasci/demeter)) was used to compute a dependency score for each gene by using the depletion values from each shRNA to infer the effect of target knockdown (on-target) and of expressing a given miRNA seed (off-target) in each cell line. More negative values indicate increased dependency, while more positive values indicate lower dependency. Zero represents the avergae dependency across all cell lines.

In the new data release, [DEMETER2](https://depmap.org/R2-D2/) ([GitHub repository](https://github.com/cancerdatasci/demeter2)), developed by McFarland et al. (2018) was used to analyze the Achilles screen. DEMETER2 expands on DEMETER by including parameters for cell-line-specific screen effects and noisy data, correcting for global differences in shRNA levels across cell lines, pooling data acorss cell lines via hierarchical modeling, and using Bayesian inference to compute uncertainty estimates. Now, a score of zero represents no dependency.

All annotation files (copy number, mutation status, and gene expression) (Consortium and Consortium 2015, Barretina et al. 2012) were downloaded from the [DepMap Data Portal](https://depmap.org/portal/download/).

## Contents

- **`data_munging`**: [Cancer Cell Line Encyclopedia (CCLE)](https://portals.broadinstitute.org/ccle) genomic annotations and rds data files produced in the Rmd
	- **`rds/`**: File format of containing serialized version of saved R object, saved with gzip compression
	- `20180817_depmap_ccl_not_in_daniel.tsv`: Cell lines not in Daniel Charytonowicz's cell line database; for searching later on
	- `CCLE_DepMap_18q3_maf_20180718.txt.gz`: Mutations
	- `D2_combined_gene_dep_scores.csv.gz`: DEMETER2 score results
	- `DepMap-2018q3-celllines.csv`: DepMap cell line metadata
	- `danielc_cell_line_database_completed_extra_SE.tsv`: Daniel Charytonowicz's cell line database
	- `gene_effect_18q3.csv.gz`: CERES score results
	- `public_18Q3_gene_cn.csv.gz`: Copy number
	- `sample_info_18Q3_crispr.csv`: CRISPR screen sample metadata
	- `sample_info_18Q3_shrna.csv`: shRNA screen sample metadata
- **`plots`**: Plots created in the Rmd
- `lineages_18Q3.Rmd`: Code to use and generate files in `data_munging` and figures in `plots`