avana_public_19Q2

This Achilles dataset contains the results of genome-scale CRISPR knockout screens for 17,634 genes in 563 cell lines. It was processed using the following steps:

- Sum raw readcounts by replicate and guide
- Remove the list of guides with suspected off-target activity
- Remove guides with pDNA counts less than one millionth of the pDNA pool
- Remove replicates that fail fingerprinting match to parent or derivative lines
- Remove replicates with total reads less than 15 million
- Remove replicates that do not have a Pearson coefficient > .7 with at least one other replicate for the line
- Calculate log2-fold-change from pDNA counts for each replicate
 - Calculate the SSMD for each cell line using guides targeting the Hart reference essentials and non-essentials, and remove those with values more positive than -0.5. See Hart et al., Mol. Syst. Biol, 2014.
- Calculate the SSMD for each cell line after averaging remaining replicates, and remove those more positive than -0.5
- Run CERES to generate gene-level scores.
- "Batch-correct" CERES data to remove known sources of bias. 
- Identify pan-dependent genes as those for whom 90% of cell lines rank the gene above a given dependency cutoff. The cutoff is determined from the central minimum in a histogram of gene ranks in their 90th percentile least dependent line.
- For each CERES gene score, infer the probability that the score represents a true dependency or not. This is done using an EM step until convergence independently in each cell line. The dependent distribution is determined empirically from the scores of the pan-dependent genes. The null distribution is determined from unexpressed gene scores in those cell lines that have expression data available, and from the Hart non-essential gene list in the remainder.

The source for copy number data varies by cell line. Copy number data  indicated as "Sanger WES" are based on the Sanger Institute whole exome sequencing data (COSMIC: http://cancer.sanger.ac.uk/cell_lines, EGA accession number: EGAD00001001039) reprocessed using CCLE pipelines. Copy number source was chosen according to the following logic:
- Broad WES for lines where available
- Broad SNP when Broad WES is not available and Sanger WES not available, or Sanger WES copy number has less correlation with logfold change than Broad SNP
- Sanger WES in all other cases


*****************
Dataset contents:
*****************

## Post-CERES files:

README - Raw

gene_effect_unscaled - NumericalMatrix
CERES-inferred gene effects without additional processing. 
Columns: genes in the format  “HUGO (Entrez)”
Rows: cell lines (Broad IDs)

gene_effect - NumericalMatrix
CERES data with principle components strongly related to known batch effects removed. 
Columns: genes in the format  “HUGO (Entrez)”
Rows: cell lines (Broad IDs)

gene_dependency - NumericalMatrix
Probability that knocking out the gene has a real depletion effect using gene_effect.
Columns: genes in the format  “HUGO (Entrez)”
Rows: cell lines (Broad IDs)

guide_efficacy - Table
Columns:
sgrna (nucleotides)
efficacy - CERES inferred efficacy for the guide

pan_dependent_genes - Table
List of genes identified as dependencies in all lines, one per line. The scores of these genes are used as the dependent distribution for inferring dependency probability.


## Pre-CERES files
essential_genes - Table
List of genes used as positive controls, currently the 217 Hart panessentials in the format “HUGO (Entrez)”. Each entry is separated by a newline.

nonessential_genes - Table
List of genes used as negative controls (Hart nonessentials) in the format “HUGO (Entrez)”. Each entry is separated by a newline.

raw_readcounts - NumericalMatrix
Summed counts for each replicate/PDNA
Columns: replicate/pDNA IDs 
Rows: Guides (nucleotides)

logfold_change - NumericalMatrix
Post-QC log2-fold change (not ZMADed)
Columns: replicate IDs
Rows: Guides (nucleotides)

guide_gene_map - Table
Columns:
sgrna (nucleotides) - appears more than once
genome_alignment
gene (“HUGO (Entrez)”)
n_alignments (integer number of perfect matches for that guide)

replicate_map - Table
Columns:
replicate_ID (str)
Broad_ID
pDNA_batch (int): indicates which processing batch the replicate belongs to and therefore which pDNA reference it should be compared with.

dropped_guides - Raw
Guides dropped for suspected off-target activity, separated by newlines.
