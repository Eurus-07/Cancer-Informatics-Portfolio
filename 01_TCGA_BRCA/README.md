# Project 01 — TCGA Breast Cancer Molecular and Clinical Analysis

## Research Question

How do molecular subtypes of breast cancer differ in clinical characteristics, survival outcomes, and gene expression patterns?

## Dataset

TCGA Breast Invasive Carcinoma (TCGA-BRCA)

Clinical data included:
- Demographics
- Tumour stage
- Pathologic TNM classification
- Survival information
- PAM50 molecular subtype

Gene expression data:
- TCGA-BRCA RNA-seq
- 981 PAM50-annotated primary tumour samples
- GENCODE v36 gene annotation

## Analysis Workflow

1. Clinical data exploration and cleaning
2. Clinical characteristic analysis
3. Overall survival analysis
4. PAM50 molecular subtype analysis
5. RNA-seq gene expression QC
6. Principal component analysis
7. Marker gene expression analysis
8. Differential expression analysis between Basal-like and Luminal A tumours

## Key Results

### Clinical and Survival Analysis

- 1098 TCGA-BRCA patients were included in the clinical dataset.
- 1094 patients were evaluable for overall survival.
- Tumour stage was significantly associated with overall survival.
- Global stage-based log-rank test:
  - Chi-square = 90.90
  - p = 1.40 × 10^-19

### PAM50 Molecular Subtypes

981 patients had PAM50 subtype annotations:

- Luminal A: 499
- Luminal B: 197
- Basal-like: 171
- HER2-enriched: 78
- Normal-like: 36

### Gene Expression Analysis

- 60,660 RNA-seq gene features were evaluated.
- 33,416 genes passed expression filtering.
- PCA was performed using the 5,000 most variable genes.
- PC1 explained 12.38% of variance.
- PC2 explained 8.73% of variance.
- PC1 + PC2 explained 21.11% of total variance.

PCA showed clear transcriptional separation of Basal-like tumours from luminal tumours.

PC1 captured a strong basal–luminal transcriptional axis:

Basal-associated genes included:
- FOXC1
- BCL11A
- VGLL1
- PSAT1

Luminal-associated genes included:
- ESR1
- FOXA1
- GATA3

### Marker Expression

Canonical subtype-associated expression patterns were recovered:

- Luminal A/B:
  - ESR1
  - PGR
  - GATA3
  - FOXA1

- HER2-enriched:
  - ERBB2

- Basal-like:
  - FOXC1
  - KRT5
  - KRT14
  - KRT17

### Differential Expression

Basal-like and Luminal A tumours were compared:

- Luminal A samples: 499
- Basal-like samples: 171
- Genes tested after filtering: 33,520
- Genes with FDR < 0.05: 25,151

Using FDR < 0.05 and absolute mean expression difference ≥ 1:

- Basal-like upregulated genes: 2,837
- Luminal A upregulated genes: 3,250
- Total large-effect differential genes: 6,087

Basal-like tumours showed increased expression of genes including:
- FOXC1
- BCL11A
- VGLL1
- KRT5
- KRT14
- KRT17

Luminal A tumours showed increased expression of:
- ESR1
- PGR
- FOXA1
- GATA3

## Key Figures

- Clinical stage distribution
- Kaplan–Meier survival curves
- PAM50 subtype distribution
- PAM50 gene-expression PCA
- PAM50 marker-expression heatmap
- Basal-like vs Luminal A volcano plot

## Tools and Skills

- Python
- pandas
- NumPy
- SciPy
- statsmodels
- scikit-learn
- matplotlib
- lifelines
- TCGA/GDC data
- UCSC Xena
- cBioPortal
- GENCODE
- Git and GitHub

## Conclusion

TCGA breast cancers display strong molecular heterogeneity across PAM50 subtypes. Basal-like tumours showed a distinct global transcriptional profile characterised by basal-associated genes, while Luminal A tumours retained strong hormone receptor and luminal differentiation programmes. The agreement between PCA, marker expression, and differential expression analyses provides consistent evidence for the biological separation of these major breast cancer subtypes.
