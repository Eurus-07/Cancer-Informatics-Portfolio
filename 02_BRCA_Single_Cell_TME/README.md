# Project 02 — Single-Cell Analysis of the Breast Cancer Tumor Microenvironment

## Overview

This project investigates the cellular composition and transcriptional heterogeneity of the tumor microenvironment in a triple-negative breast cancer (TNBC) sample using single-cell RNA sequencing.

The analysis focuses on the CID4465 breast cancer sample and applies a Scanpy-based workflow to characterize major tumor microenvironment compartments, including immune, stromal, endothelial, and malignant epithelial populations.

## Dataset

- Sample: CID4465
- Cancer subtype: Triple-negative breast cancer (TNBC)
- Data type: Single-cell RNA sequencing
- Initial cells: 1,564
- Cells retained after QC: 1,534
- Genes retained after filtering: 13,514

## Analysis Workflow

### 01 — Data Loading and Quality Control

The raw single-cell expression matrix and metadata were imported into an AnnData object.

Quality-control metrics included:

- Number of detected genes per cell
- Total transcript counts
- Mitochondrial transcript percentage

QC filtering retained 1,534 of 1,564 cells.

Highly variable genes were identified, followed by PCA, neighborhood graph construction, Leiden clustering, and UMAP visualization.

---

### 02 — Cell-Type Validation

Original metadata annotations were examined and compared with transcriptional clusters.

Major cellular compartments included:

- Cancer epithelial cells
- T cells
- B cells
- Plasmablasts
- Myeloid cells
- Cancer-associated fibroblasts
- Perivascular-like cells
- Endothelial cells
- Normal epithelial cells

Cluster-specific marker genes were used to assess biological consistency of the supplied cell-type annotations.

---

### 03 — Immune Microenvironment

The immune compartment was examined in greater detail.

Major immune populations included:

- CD4+ T cells
- CD8+ T cells
- Regulatory T cells
- NKT and NK cells
- Monocytes
- Macrophages
- Dendritic cells
- B cells
- Plasmablasts

Immune transcriptional programmes were evaluated to explore heterogeneity within lymphoid and myeloid populations.

---

### 04 — Stromal Microenvironment

The stromal compartment was analysed separately.

Major stromal populations included:

- myCAF-like cancer-associated fibroblasts
- MSC/iCAF-like fibroblasts
- Perivascular-like cells
- Endothelial populations

The analysis examined stromal-state composition and transcriptional diversity within the TNBC tumor microenvironment.

---

### 05 — Tumor and Epithelial Heterogeneity

Cancer epithelial cells were isolated for tumor-only re-clustering.

A total of 113 cancer epithelial cells were analysed.

Original tumor annotations included:

- Cancer Cycling: 89 cells
- Cancer Basal SC: 19 cells
- Cancer LumB SC: 5 cells

Tumor-specific highly variable genes were selected and used for PCA, neighborhood graph construction, UMAP, and Leiden clustering.

At Leiden resolution 0.5, three exploratory transcriptional states were identified:

- Intermediate epithelial: 40 cells
- Stress-responsive epithelial: 31 cells
- Proliferative: 42 cells

No individual cluster-marker genes remained statistically significant after multiple-testing correction.

Gene-program analysis showed a significant difference in proliferation activity across the three tumor states:

- Kruskal-Wallis H = 6.559
- p = 0.0376

Basal, epithelial, and stress-associated programme scores were not significantly different across clusters.

These results suggest that the malignant compartment displays continuous functional heterogeneity rather than strongly separated tumor subtypes.


### 06 — Cell–Cell Communication

Potential ligand–receptor interactions among major tumor microenvironment
compartments were explored using LIANA.

The analysis included:

- Cancer epithelial cells
- CAFs
- Perivascular-like cells
- Endothelial cells
- Myeloid cells
- T cells
- B cells
- Plasmablasts

Normal epithelial cells were excluded from the main communication analysis
because of their small cell number.

A total of 615 tumor-centered ligand–receptor interactions were identified.
After excluding tumor self-signaling and applying exploratory consensus-ranking
thresholds, 9 high-ranking tumor–TME candidate interactions were retained.

Two recurrent communication patterns emerged.

#### Stromal/endothelial → tumor signaling

Multiple stromal and endothelial ligands converged on ITGB1-containing
receptors in cancer epithelial cells.

Notable candidate interactions included:

- CAFs → Cancer Epithelial: LUM → ITGB1
- Endothelial → Cancer Epithelial: VWF → ITGB1

Additional ITGB1-associated candidate ligands included LGALS1, HSPG2, VCAN,
LGALS3BP, CLEC11A, SPON2, FBLN1, TGM2, LAMA4, and LAMC1.

#### Tumor → stromal signaling

MDK emerged as a recurrent candidate tumor-derived ligand targeting several
stromal compartments:

- Cancer Epithelial → PVL: MDK → SDC2
- Cancer Epithelial → CAFs: MDK → LRP1
- Cancer Epithelial → Endothelial: MDK → ITGA6_ITGB1

Additional candidate tumor–immune interactions included:

- CD59 → CD2
- COPA → CD74
- S100A8 → CD68
- S100A8 → CD69

Because this analysis is based on ligand–receptor expression inference from a
single tumor sample, these interactions are interpreted as candidate
communication events rather than experimentally validated signaling activity.

---

### 07 — Myeloid Trajectory and Diffusion Pseudotime

The myeloid compartment was further investigated to assess transcriptional
continuity between monocyte- and macrophage-associated states.

The original myeloid compartment contained 178 cells:

- Macrophage: 109
- Monocyte: 36
- Cycling myeloid: 21
- Dendritic cells: 12

For trajectory analysis, monocytes and macrophages were analysed separately,
resulting in a 145-cell monocyte–macrophage compartment.

Diffusion-map analysis suggested a continuous rather than sharply separated
monocyte–macrophage transcriptional landscape.

A biologically informed pseudotime root was selected from the
IL1B-associated monocyte population using high monocyte-program and low
macrophage-program activity.

Subset pseudotime ordering showed an overall progression from:

- S100A9-associated monocytes
- IL1B-associated monocytes
- LAM1/FABP5 macrophages
- CXCL10-associated macrophages
- EGR1-associated macrophages

Macrophage-associated transcriptional activity showed a weak but statistically
significant positive correlation with pseudotime:

- Spearman rho = 0.178
- p = 0.0323

The monocyte-associated programme showed a non-significant decreasing trend:

- Spearman rho = -0.102
- p = 0.2205

These results support an exploratory monocyte-to-macrophage transcriptional
continuum, but do not constitute direct evidence of temporal differentiation
or lineage fate.
---

### 08 — Computational Method Benchmarking

Clustering strategies were benchmarked to evaluate how algorithmic choice affects recovery of biologically annotated cell populations in TNBC single-cell RNA-seq data.

A common computational representation was constructed using:

- 1,534 cells
- 2,000 highly variable genes
- Scaled gene expression
- 50 principal components

Two clustering strategies were compared using the same PCA representation:

- K-means clustering (k = 9)
- Leiden graph-based clustering (resolution = 0.5)

Performance was evaluated using Adjusted Rand Index (ARI), Normalized Mutual Information (NMI), cluster purity, silhouette score, cluster composition, and parameter sensitivity.

#### Quantitative benchmarking

K-means produced nine clusters:

- ARI = 0.772
- NMI = 0.866
- Purity = 0.953
- Silhouette = 0.074

Leiden produced seven clusters:

- ARI = 0.909
- NMI = 0.890
- Purity = 0.930
- Silhouette = 0.072

Leiden therefore showed substantially stronger overall agreement with the biological cell-type annotations despite producing fewer clusters.

K-means achieved slightly higher cluster purity, but cluster-composition analysis showed that several biological populations, particularly CAFs and perivascular-like cells, were split across multiple K-means clusters. This demonstrates why cluster purity alone can be misleading when evaluating clustering performance.

Leiden more consistently recovered major CAF, perivascular, endothelial, myeloid, and cancer epithelial populations, although some closely related lymphoid populations were merged.

#### Leiden resolution sensitivity

Leiden resolution was systematically evaluated from 0.2 to 1.0 while keeping the underlying nearest-neighbour graph fixed.

Resolutions 0.3–0.5 produced the same stable seven-cluster solution and achieved the strongest agreement with biological annotations:

- ARI = 0.909
- NMI = 0.890

Increasing the resolution to 0.6–1.0 generated eight to nine clusters but reduced ARI and NMI, indicating that increased clustering granularity did not improve biological recovery.

Overall, this benchmarking analysis demonstrates that clustering methods should be evaluated using multiple complementary metrics rather than cluster number or visual separation alone. In this dataset, graph-based Leiden clustering provided stronger correspondence with biological cell identities than centroid-based K-means clustering.

## Key Findings

1. The CID4465 TNBC microenvironment contains substantial immune, stromal, endothelial, and malignant epithelial heterogeneity.

2. Stromal populations, particularly CAFs and perivascular-like cells, represent major components of the tumor microenvironment.

3. Tumor epithelial cells display continuous functional heterogeneity, with proliferation representing the clearest programme distinguishing exploratory tumor-cell states.

4. Cell–cell communication analysis identified candidate stromal–tumor signaling patterns, including recurrent ITGB1-associated interactions and tumor-derived MDK signaling.

5. Myeloid trajectory analysis supported an exploratory monocyte-to-macrophage transcriptional continuum, while emphasizing that pseudotime does not directly establish temporal differentiation or lineage fate.

6. Computational benchmarking showed that graph-based Leiden clustering recovered biological cell identities more consistently than K-means clustering (ARI 0.909 vs 0.772), despite K-means achieving slightly higher cluster purity.

7. Leiden resolution sensitivity analysis identified a stable solution across resolutions 0.3–0.5, demonstrating that increased cluster granularity does not necessarily improve biological recovery.

8. Together, these analyses illustrate the importance of combining biological interpretation with quantitative evaluation of computational methods in single-cell cancer genomics.

## Repository Structure

```text
02_BRCA_Single_Cell_TME/
├── data/
│   ├── raw/
│   └── processed/
├── figures/
├── notebooks/
│   ├── 01_data_loading_and_qc.ipynb
│   ├── 02_cell_type_validation.ipynb
│   ├── 03_immune_microenvironment.ipynb
│   ├── 04_stromal_microenvironment.ipynb
│   ├── 05_tumor_epithelial_heterogeneity.ipynb
│   ├── 06_cell_cell_communication.ipynb
│   ├── 07_myeloid_trajectory.ipynb
│   └── 08_computational_method_comparison.ipynb
├── results/
└── README.md