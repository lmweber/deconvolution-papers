# deconvolution-papers

A number of algorithms have recently been developed for deconvolution of cell types in bulk RNA-seq samples based on cell type signatures derived from single-cell RNA-seq data. This repository contains a list of recent algorithms, benchmark papers, and application papers, along with our comments on them.

The list is organized into three parts: (i) method papers describing algorithms, (ii) benchmark papers, and (iii) application papers. The list will be added to over time.



## Method papers

Method | Reference | Availability | Comments
:----- | :-------- | :----------- | :-------
Bisque | [Jew et al. (2019), bioRxiv](https://www.biorxiv.org/content/10.1101/669911v1) | [R package](https://github.com/cozygene/bisque) from GitHub. | Uses psuedo bulk (adding up single cells) vs actual bulk and then does a transformation. Methods section could be improved. 
CIBERSORT | [Newman et al. (2015), Nature Methods](https://www.nature.com/articles/nmeth.3337) | [Online tool](https://cibersort.stanford.edu/) requiring signup and login. | Requires input matrix of reference gene expression signatures for cell types. Methodology is based on linear support vector regression, which also performs feature selection on the genes in the signature matrix. Also returns overall p-value for null hypothesis that no cell types from the signature matrix are present. Extensive benchmarking on datasets with both simulated and experimental (e.g. flow sorted) ground truth, and comparison against several earlier methods (using microarray data only). Currently appears to be the most widely used tool.
CIBERSORTx | [Newman et al. (2019), Nature Biotechnology](https://www.nature.com/articles/s41587-019-0114-2) | [Online tool](https://cibersortx.stanford.edu/) requiring signup and login. Free for academic use only. | 
DWLS | [Tsoucas et al. (2019), Nature Communications](https://www.nature.com/articles/s41467-019-10802-z) | [R package](https://bitbucket.org/yuanlab/dwls/src/default/) from BitBucket. | 
EPIC | [Racle et al. (2017), eLife](https://elifesciences.org/articles/26476) | [R package](https://github.com/GfellerLab/EPIC) from GitHub, as well as [web application](http://epic.gfellerlab.org/). | 
MuSiC | [Wang et al. (2019), Nature Communications](https://www.nature.com/articles/s41467-018-08023-x) | [R package](https://github.com/xuranw/MuSiC) from GitHub. | 
Scaden | [Menden et al. (2019), bioRxiv](https://www.biorxiv.org/content/10.1101/659227v1) | [Python 3 package](https://github.com/KevinMenden/scaden) from Bioconda and PyPI. | 



## Benchmark papers

Papers describing existing benchmarking studies comparing some of the above methods.


Paper | Description
:---- | :----------
[Sturm et al. (2019), Bioinformatics](https://academic.oup.com/bioinformatics/article/35/14/i436/5529146#.XS2eAAl_aaE.twitter) | Benchmark with reproducible code provided as a Snakemake pipeline. Uses datasets consisting of immune cell populations in the tumor microenvironment (TME).
[Huang et al. (2019), bioRxiv](https://www.biorxiv.org/content/10.1101/827139v1) | Benchmarked 8 methods developed for single-cell RNA-seq (Seurat, scmap, SingleR, CHETAH, SingleCellNet, scID, Garnett, SCINA) and 2 for DNAm (Linear Constrained Projection (CP) and Robust Partial Correlations (RPC))



## Application papers

Application papers listed here will be mainly from the field of ovarian cancer.


Paper | Description
:---- | :----------
[Hu et al. (2019), bioRxiv](https://www.biorxiv.org/content/10.1101/672626v1) | Non-genetic heterogeneity (NGH) within tumors (i.e. heterogeneity related to different cell types, as opposed to genetic heterogeneity due to mutations) is associated with tumor resilience but difficult to quantify. The authors perform scRNA-seq on 4000 normal fallopian tube epithelial (FTE) cells from 11 donors to identify 6 FTE subpopulations; FTE cells are the cells of origin for serous ovarian cancer (SOC). They then use the gene expression signatures of 5 FTE subtypes to deconvolve SOC expression data from bulk samples to identify NGH within tumors, and stratify subtypes of SOC based on NGH. Cell types within the scRNA-seq data are identified by clustering and differential expression based annotation according to known marker genes (note they used a customized clustering algorithm). Deconvolution is done using the CIBERSORT algorithm. The stratified SOC subtypes are shown to predict survival in a dataset of 1700 bulk tumor samples from The Cancer Genome Atlas (TCGA) and Australian Ovarian Cancer Study (AOCS). An open question is whether NGH is due to multiple cell types of origin for the tumor, or due to differentiation within the tumor, or a combination of both.
[Schwede et al. (2018), bioRxiv](https://www.biorxiv.org/content/10.1101/496406v1) | **Main conclusions**: Demonstrates (1) HGSOC subtype identification depends on ratio of tumor to stroma within the specimen and (2) The anatomic location of biopsy may influence the proportion of stromal involvement and potentially the resulting gene expression pattern. Also important to define the relative proportions of stromal cells and model their prognostic importance in the tumor microenvironment. **Summary of data analyses**: Identified ?stromal gene set? and ?tumor gene sets" using two datasets (AOCS n=8 and TCGA n=38 paired tumors). Found overlap in genes between two datasets (found 23 tumor genes and 125 stroma genes). Performed unsupervised clustering: Found that microdissected tumor samples cluster with bulk C4/C5 subtype and and microdissected stroma samples cluster with bulk C1/C2 subtype. Found gene signature classifiers for AOCS and TCGA molecular subtypes are not stable when the proportion of stromal cells changes. Found pathologist scores of percent of stromal content was associated with overall survival (Cox PH) in high stage (III or IV) tumors. Using n=61 published prognostic ovarian gene signatures from GeneSigDB, found 24/61 were enriched for AOCS stromal genes and 11/61 were enriched in MGH stroma genes. 8 were sets of signatures were strongly enriched in both datasets. Stroma signature is not specific to HGSOC. Also found these signatures in breast and prostate. The sampling location of tumors (extra-ovarian vs ovary/pelvis) impacts the stroma?s prognostic power 



