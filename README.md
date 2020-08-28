# deconvolution-papers

A number of algorithms have recently been developed for deconvolution of cell types in bulk RNA-seq samples based on cell type signatures from matched single-cell RNA-seq samples or other marker gene lists.

This repository lists recent method papers, benchmark papers, and application papers using deconvolution algorithms, along with some of our comments.


## Method papers

Method | Reference | Availability | Comments
:----- | :-------- | :----------- | :-------
Bisque | [Jew et al. (2020), Nature Communications](https://www.nature.com/articles/s41467-020-15816-6) | [R package from GitHub](https://github.com/cozygene/bisque) | Uses pseudo-bulk (adding up single cells) vs actual bulk and then does a transformation. Methods section could be improved.
CIBERSORT | [Newman et al. (2015), Nature Methods](https://www.nature.com/articles/nmeth.3337) | [Online tool requiring signup and login](https://cibersort.stanford.edu/) | Requires input matrix of reference gene expression signatures for cell types. Methodology is based on linear support vector regression, which also performs feature selection on the genes in the signature matrix. Also returns overall p-value for null hypothesis that no cell types from the signature matrix are present. Extensive benchmarking on datasets with both simulated and experimental (e.g. flow sorted) ground truth, and comparison against several earlier methods (using microarray data only). Widely used in application papers, but not easily accessible or reproducible (only available as online tool requiring signup and login).
CIBERSORTx | [Newman et al. (2019), Nature Biotechnology](https://www.nature.com/articles/s41587-019-0114-2) | [Online tool requiring signup and login](https://cibersortx.stanford.edu/). | Extension of previous tool CIBERSORT. Not easily accessible or reproducible (only available as online tool requiring signup and login). Free for academic use only (not commercial), which limits usefulness.
DWLS | [Tsoucas et al. (2019), Nature Communications](https://www.nature.com/articles/s41467-019-10802-z) | [R package from BitBucket](https://bitbucket.org/yuanlab/dwls/src/default/) | 
EPIC | [Racle et al. (2017), eLife](https://elifesciences.org/articles/26476) | [R package from GitHub](https://github.com/GfellerLab/EPIC), as well as [web application](http://epic.gfellerlab.org/) | 
MuSiC | [Wang et al. (2019), Nature Communications](https://www.nature.com/articles/s41467-018-08023-x) | [R package from GitHub](https://github.com/xuranw/MuSiC) | 
Scaden | [Menden et al. (2020), Science Advances](https://advances.sciencemag.org/content/6/30/eaba2619) | [Python package from Bioconda and PyPI](https://github.com/KevinMenden/scaden), as well as [web application](https://scaden.ims.bio/) | 


## Benchmark papers

Paper | Description
:---- | :----------
[Patrick et al. (2020), PLOS Computational Biology](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1008120) | Benchmark of deconvolution algorithms to estimate cell type proportions in brain tissue. Experimentally generated immunohistochemistry (IHC) benchmark dataset (5 major cell types, 70 individuals, with matched bulk cortical gene expression data). Deconvolution algorithms are run using known marker gene sets. Algorithms in benchmark include: NNLS, CIBERSORT, dtangle, DSA, MuSiC, BSEQ-sc.
[Cobos et al. (2020), bioRxiv](https://www.biorxiv.org/content/10.1101/2020.01.10.897116v1) | 
[Huang et al. (2020), bioRxiv](https://www.biorxiv.org/content/10.1101/827139v2) | Benchmarked 8 methods developed for single-cell RNA-seq (Seurat, scmap, SingleR, CHETAH, SingleCellNet, scID, Garnett, SCINA) and 2 for DNAm (Linear Constrained Projection (CP) and Robust Partial Correlations (RPC))
[Sturm et al. (2019), Bioinformatics](https://academic.oup.com/bioinformatics/article/35/14/i436/5529146) | Benchmark with reproducible code provided as a Snakemake pipeline. Uses datasets consisting of immune cell populations in the tumor microenvironment (TME).


## Application papers

Mainly from the field of ovarian cancer, since this is the application area we are working on.

Paper | Description
:---- | :----------
[Hu et al. (2020), Cancer Cell](https://www.sciencedirect.com/science/article/pii/S1535610820300428) | Non-genetic heterogeneity (NGH) within tumors (i.e. heterogeneity related to different cell types, as opposed to genetic heterogeneity due to mutations) is associated with tumor resilience but difficult to quantify. The authors perform scRNA-seq on 4000 normal fallopian tube epithelial (FTE) cells from 11 donors to identify 6 FTE subpopulations; FTE cells are the cells of origin for serous ovarian cancer (SOC). They then use the gene expression signatures of 5 FTE subtypes to deconvolve SOC expression data from bulk samples to identify NGH within tumors, and stratify subtypes of SOC based on NGH. Cell types within the scRNA-seq data are identified by clustering and differential expression based annotation according to known marker genes (note they used a customized clustering algorithm). Deconvolution is done using the CIBERSORT algorithm. The stratified SOC subtypes are shown to predict survival in a dataset of 1700 bulk tumor samples from The Cancer Genome Atlas (TCGA) and Australian Ovarian Cancer Study (AOCS). An open question is whether NGH is due to multiple cell types of origin for the tumor, or due to differentiation within the tumor, or a combination of both.
[Schwede et al. (2020), Cancer Epidemiology, Biomarkers & Prevention](https://cebp.aacrjournals.org/content/29/2/509) | **Main conclusions**: Demonstrates (1) HGSOC subtype identification depends on ratio of tumor to stroma within the specimen and (2) The anatomic location of biopsy may influence the proportion of stromal involvement and potentially the resulting gene expression pattern. Also important to define the relative proportions of stromal cells and model their prognostic importance in the tumor microenvironment. **Summary of data analyses**: Identified "stromal gene set" and "tumor gene sets" using two datasets (AOCS n=8 and TCGA n=38 paired tumors). Found overlap in genes between two datasets (found 23 tumor genes and 125 stroma genes). Performed unsupervised clustering: Found that microdissected tumor samples cluster with bulk C4/C5 subtype and and microdissected stroma samples cluster with bulk C1/C2 subtype. Found gene signature classifiers for AOCS and TCGA molecular subtypes are not stable when the proportion of stromal cells changes. Found pathologist scores of percent of stromal content was associated with overall survival (Cox PH) in high stage (III or IV) tumors. Using n=61 published prognostic ovarian gene signatures from GeneSigDB, found 24/61 were enriched for AOCS stromal genes and 11/61 were enriched in MGH stroma genes. 8 were sets of signatures were strongly enriched in both datasets. Stroma signature is not specific to HGSOC. Also found these signatures in breast and prostate. The sampling location of tumors (extra-ovarian vs ovary/pelvis) impacts the stroma's prognostic power.

