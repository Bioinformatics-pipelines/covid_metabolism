# covid_metabolism

This repository contains the code for reproducing the analyses in:

Cheng et al. Genome-scale metabolic modeling reveals SARS-CoV-2-induced host metabolic reprogramming and identifies metabolic antiviral targets.

## 1. Prerequisites

### Softwares

* R 3.6 (R 3.6.3 was used in our study)
* R packages
  - ImNotaGit/my.utils
  - ruppinlab/Rcplex2: required to run genome-scale metabolic modeling (GEM); otherwise may be omitted
  - ruppinlab/gembox
  - other needed packages can be obtained from CRAN or Bioconductor, please see the R scripts
* IBM ILOG CPLEX Optimization Studio or Gurobi: required to run GEM; otherwise may be omitted (CPLEX 12.10 was used in our study)

### Data

The required data can be downloaded by running the `dnload.sh` bash script in the `data` folder. `dnload.sh` uses `wget` and `gdown` (the latter used for downloading files from Google Drive and can be installed with `pip install gdown`). Data files containing results from the various analyses are also included in the download.

Alternatively, one can manually download the data files from [this Google Drive link](https://drive.google.com/file/d/1bVPCQlDR3G8TTMx09jkN3IuGwzq9n9hi/view?usp=sharing) then decompress them into the `data` folder. The two single-cell RNA-sequencing datasets from Liao et al. and Chua et al. are quite large and not included in this download. Check `dnload.sh` for details on how these two datasets should be downloaded.

## 2. Description of folders and files

The scripts should be run in the same order as they are introduced below.

### data

All required data should be saved in this folder.

* `dnload.sh`: a bash script for downloading the required data
* `collect.validation.data.R`: prepare the data for validating the MTA prediction

### expression

Scripts for gene expression-level analysis: 

* `de.and.gsea.R`: differential expression (DE) and gene set enrichment analysis (GSEA) between the SARS-CoV-2-infected samples and non-infected controls in each dataset 
* `de.and.gsea.remdesivir.R`: DE and GSEA analysis for the Vero E6 cell remdesivir treatment data

### GEM

Scripts for genome-scale metabolic modeling (GEM) analysis:

* `prepare.data.R`: prepare data for GEM
* `imat.and.mta.R`: run iMAT and MTA on each dataset
* `dflux.R`: differential flux analysis between the SARS-CoV-2-infected samples and non-infected controls in each dataset 
* `collect.results.R`: collect the differential flux analysis and MTA results across datasets

### GEM_remdesivir

Scripts for GEM analysis on the Vero E6 cell remdesivir treatment data

* `prepare.data.R`: prepare data for GEM
* `imat.R`: run iMAT for each experimental group
* `mta.R`: run MTA for pairs of experimental groups
* `dflux.R`: differential flux analysis between pairs of experimental groups
* `collect.results.R`: collect the differential flux analysis results

### analyze_results

Scripts and R notebooks for inspecting the results from various analyses and for validating the MTA predictions:

* `functions.R`: various functions, will be sourced in check.mta.results.R and check.mta.results.remdesivir.R
* `check.mta.results.R`: various validations and pathway enrichment analysis of MTA results
* `check.mta.results.remdesivir.R`: various validations and pathway enrichment analysis of MTA results for predicting combinatory target with remdesivir
* Various `.Rmd` files: R notebook for inspecting and visualizing results from different analyses, see their contents for details
