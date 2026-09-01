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

## Key Findings

1. The CID4465 TNBC microenvironment contains substantial immune, stromal, endothelial, and malignant epithelial diversity.

2. Stromal cells constitute a major component of the tumor microenvironment, particularly CAF and perivascular populations.

3. Immune populations include heterogeneous lymphoid and myeloid subsets.

4. Tumor-only analysis identified three exploratory transcriptional states.

5. Proliferation was the clearest transcriptional programme distinguishing tumor-cell states.

6. Limited differential-expression significance within the malignant compartment highlights the importance of cautious interpretation when analysing small single-cell populations.

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
│   └── 05_tumor_epithelial_heterogeneity.ipynb
├── results/
└── README.md
---

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