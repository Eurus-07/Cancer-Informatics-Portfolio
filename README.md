# Cancer Informatics Portfolio

Computational cancer biology portfolio integrating clinical genomics, bulk transcriptomics, and single-cell RNA sequencing to investigate tumour heterogeneity and the tumour microenvironment.

## About

This repository documents a series of computational cancer research projects developed using public genomic, transcriptomic, clinical, and single-cell datasets.

My interests lie at the interface of cancer biology and computational analysis, particularly in understanding molecular and cellular heterogeneity, tumour–microenvironment interactions, and the quantitative evaluation of computational methods.

The portfolio progresses from patient-level clinical and transcriptomic analysis to single-cell characterisation of the tumour microenvironment, while incorporating statistical analysis, dimensionality reduction, clustering, trajectory inference, cell–cell communication analysis, and computational method benchmarking.

---

## Projects

### 01 — TCGA Breast Cancer: Clinical and Transcriptomic Heterogeneity

**Dataset:** TCGA Breast Invasive Carcinoma (TCGA-BRCA)

An integrated analysis of clinical characteristics, molecular subtypes, survival outcomes, and bulk RNA-seq profiles in breast cancer.

#### Analyses

- Clinical cohort characterisation
- Overall survival and stage-stratified survival analysis
- PAM50 molecular subtype analysis
- RNA-seq preprocessing and gene filtering
- Principal component analysis
- Breast cancer marker-gene expression analysis
- Differential expression between Luminal A and Basal-like tumours
- Multiple-testing correction and biological interpretation

#### Selected findings

- PAM50 molecular subtype annotations were available for 981 patients.
- Molecular subtype was significantly associated with patient age and tumour stage.
- Global survival differed across PAM50 subtypes, although pairwise comparisons did not remain significant after multiple-testing correction.
- Basal-like and Luminal A tumours showed extensive transcriptional differences.
- Canonical basal markers including FOXC1, KRT5, KRT14, and KRT17 and luminal markers including ESR1, PGR, FOXA1, and GATA3 showed subtype-associated expression patterns.

**Methods:** Python · pandas · survival analysis · RNA-seq · PCA · differential expression · multiple-testing correction

[Explore Project 01](./01_TCGA_BRCA/)

---

### 02 — TNBC Single-Cell Tumour Microenvironment

**Dataset:** CID4465 triple-negative breast cancer single-cell RNA-seq

A single-cell investigation of cellular heterogeneity, tumour–microenvironment organisation, intercellular communication, myeloid transcriptional trajectories, and computational clustering strategies.

#### Analyses

- Single-cell quality control and preprocessing
- Highly variable gene selection and dimensionality reduction
- PCA, neighbourhood graph construction, Leiden clustering, and UMAP
- Cell-type annotation validation
- Immune microenvironment analysis
- Stromal microenvironment analysis
- Tumour epithelial heterogeneity
- Ligand–receptor communication inference
- Myeloid diffusion pseudotime analysis
- Computational clustering benchmark

#### Selected findings

The analysed TNBC tumour contained substantial malignant, stromal, endothelial, and immune heterogeneity.

Tumour-centred ligand–receptor analysis identified candidate communication patterns including recurrent ITGB1-associated stromal–tumour interactions and tumour-derived MDK signalling.

Myeloid diffusion analysis supported an exploratory transcriptional continuum between monocyte- and macrophage-associated states while highlighting the limitations of interpreting pseudotime as direct lineage evidence.

#### Computational method benchmarking

K-means and graph-based Leiden clustering were compared using the same PCA representation of 1,534 cells and 2,000 highly variable genes.

Performance was evaluated using:

- Adjusted Rand Index (ARI)
- Normalized Mutual Information (NMI)
- Cluster purity
- Silhouette score
- Cluster composition
- Leiden resolution sensitivity

Leiden showed stronger overall correspondence with biological cell-type annotations:

| Method | Clusters | ARI | NMI | Purity | Silhouette |
| --- | ---: | ---: | ---: | ---: | ---: |
| K-means | 9 | 0.772 | 0.866 | 0.953 | 0.074 |
| Leiden | 7 | 0.909 | 0.890 | 0.930 | 0.072 |

Resolution sensitivity analysis identified a stable Leiden solution across resolutions 0.3–0.5. Increasing clustering granularity did not improve biological agreement, illustrating the importance of evaluating computational methods using multiple complementary metrics rather than cluster number or visual separation alone.

**Methods:** Python · Scanpy · AnnData · scRNA-seq · PCA · UMAP · Leiden · K-means · ARI/NMI · LIANA · diffusion pseudotime · statistical analysis

[Explore Project 02](./02_BRCA_Single_Cell_TME/)

---

## Computational Skills Demonstrated

### Data analysis and statistics

- Data cleaning and integration
- Exploratory data analysis
- Statistical hypothesis testing
- Survival analysis
- Multiple-testing correction
- Quantitative model and method evaluation

### Transcriptomics and cancer genomics

- Bulk RNA-seq analysis
- Single-cell RNA-seq analysis
- Differential gene expression
- Molecular subtype analysis
- Tumour microenvironment characterisation
- Ligand–receptor inference
- Trajectory and pseudotime analysis

### Computational methods

- Principal component analysis
- k-nearest-neighbour graph construction
- K-means clustering
- Leiden community detection
- UMAP
- Clustering evaluation using ARI, NMI, purity, and silhouette scores
- Hyperparameter sensitivity analysis

### Tools

Python · pandas · NumPy · SciPy · scikit-learn · Scanpy · AnnData · LIANA · matplotlib · Git · GitHub · Jupyter · VS Code · command line

---

## Research Focus

I am particularly interested in applying computational approaches to understand cancer heterogeneity, tumour evolution, tumour–microenvironment interactions, and treatment-relevant biological variation.

These projects are intended not only to apply established bioinformatics workflows, but also to critically evaluate computational assumptions, parameter choices, statistical evidence, and biological interpretation.