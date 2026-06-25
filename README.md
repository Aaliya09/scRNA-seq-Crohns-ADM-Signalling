# Single-Cell RNA-Seq Analysis of Adrenomedullin (ADM) Signalling in Crohn's Disease

**Graduate Research | APC Microbiome Ireland, University College Cork**

[![R](https://img.shields.io/badge/R-Seurat%20v5-276DC3?logo=r)](https://satijalab.org/seurat/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## Overview

A comprehensive single-cell RNA sequencing (scRNA-Seq) study investigating **adrenomedullin (ADM) signalling** across the full cellular landscape of the human intestine in Crohn's disease. This is one of the first studies to systematically profile ADM receptor components — CALCRL, RAMP2, RAMP3, and ACKR3 — at single-cell resolution across multiple intestinal compartments, tissue sites, and patient cohorts.

### Study Design

| Dimension | Groups |
|-----------|--------|
| **Tissue sites** | Terminal Ileum (TI) · Colon |
| **Cell compartments** | Stromal · Epithelial · Immune |
| **Patient cohorts** | Adult · Paediatric |
| **Conditions** | Healthy · Crohn's Non-Inflamed (NonI) · Crohn's Inflamed (Infl) |

This multi-dataset design enables cross-site, cross-compartment, and cross-cohort comparisons of ADM signalling dysregulation in intestinal inflammation.

---

## Research Questions

- How is ADM signalling altered across intestinal cell compartments in Crohn's disease?
- Do stromal, epithelial, and immune cells show distinct ADM receptor expression patterns?
- Are ADM signalling changes consistent between adult and paediatric Crohn's disease?
- What downstream KEGG pathways are enriched in inflamed vs. healthy conditions per cell type?

---
Raw counts matrix (.mtx / .rds)

│

▼

01. QC & Preprocessing

├── Mitochondrial % filtering

├── Feature / count thresholding

└── Normalisation (log-norm + ScaleData)

│

▼

02. Integration & Dimensionality Reduction

├── Highly variable features (VST, top 2000)

├── Harmony batch correction (across samples/conditions)

├── PCA + elbow plot

└── UMAP (dims 1:10)

│

▼

03. Clustering & Cell Type Annotation

├── Graph-based clustering (Louvain)

├── Cell type annotation from published markers

├── Metadata integration (condition, site, cohort)

└── Cell proportion analysis across conditions

│

▼

04. ADM Signalling Expression Analysis

├── FeaturePlot, VlnPlot, DotPlot per cell type

├── Condition-stratified dot plots (Healthy / NonI / Infl)

└── Per-gene expression quantification (% expressing cells)

│

▼

05. Differential Expression (MAST)

├── Per-cell-type DE: Healthy vs NonI, Healthy vs Infl, NonI vs Infl

├── Gene filtering (≥10% cells expressing per group)

└── Adjusted p-value threshold: 0.05

│

▼

06. Pathway Enrichment & Visualisation

├── KEGG enrichment — up- and downregulated DEGs (clusterProfiler)

├── Gene symbol → Entrez ID mapping (org.Hs.eg.db)

└── Pathway-level visualisation (pathview, 17 KEGG pathways)

---

## Repository Structure
scRNA-seq-Crohns-ADM-Signalling/

│

├── TI_Stromal/

│   ├── 01_QC_preprocessing.R

│   ├── 02_clustering_annotation.R

│   ├── 03_ADM_expression.R

│   ├── 04_MAST_DE.R

│   └── 05_KEGG_pathview.R

│

├── TI_Epithelial/

│   └── ...

│

├── TI_Immune/

│   └── ...

│

├── Colon_Stromal/

│   └── ...

│

├── Colon_Epithelial/

│   └── ...

│

├── Colon_Immune/

│   └── ...

│

├── Paediatric/

│   └── ...

│

├── results/

│   └── figures/                   # UMAP plots, dot plots, KEGG figures

│

├── environment/

│   └── sessionInfo.txt            # R session info for reproducibility

│

└── README.md

---

## Key Genes Analysed

| Gene | Role |
|------|------|
| ADM | Adrenomedullin — vasodilatory, anti-inflammatory peptide |
| CALCRL | Core ADM receptor subunit |
| RAMP2 | Receptor activity-modifying protein 2 (ADM receptor complex) |
| RAMP3 | Receptor activity-modifying protein 3 (ADM receptor complex) |
| ACKR3 | Atypical chemokine receptor 3 — ADM scavenging receptor |
| ICAM1, VCAM1, SELE | Endothelial inflammation markers |
| TNF, IL6 | Pro-inflammatory cytokines |
| CXCR7, CRCP, GPR182 | Additional ADM/ACKR3 pathway components |

---

## Cell Compartments & Representative Cell Types

### Stromal (Terminal Ileum & Colon)
16 annotated subtypes including: Fibroblasts (ADAMDEC1, SMOC2/PTGIS, SFRP2/SLPI, NPY/SLITRK6, KCNN3/LY6H, Activated CCL19), Endothelial cells (CD36, DARC, CA4/CD36, LTC4S/SEMA3G), Myofibroblasts (HHIP/NPNT, GREM1/GREM2), Pericytes (HIGD1B/STEAP4, RERGL/NTRK2), Glial cells, Lymphatics

### Epithelial (Terminal Ileum & Colon)
Enterocytes, Goblet cells, Paneth cells, Enteroendocrine cells, Tuft cells, Stem cells, Transit-amplifying cells

### Immune (Terminal Ileum & Colon)
T cells, B cells, Macrophages, Dendritic cells, NK cells, Mast cells, Plasma cells, Neutrophils

---

## Methods Summary

| Step | Tool / Method |
|------|--------------|
| Data format | Matrix Market (.mtx), sparse matrix, RDS |
| Seurat version | v5 |
| Normalisation | Log-normalisation + ScaleData |
| Dimensionality reduction | PCA, UMAP |
| Clustering | Louvain (FindNeighbors + FindClusters) |
| Batch correction | Harmony |
| Differential expression | MAST (via Seurat FindMarkers) |
| Pathway enrichment | clusterProfiler (enrichKEGG) |
| Pathway visualisation | pathview (17 KEGG pathways) |
| Gene ID mapping | org.Hs.eg.db (SYMBOL → ENTREZID) |
| Visualisation | ggplot2, patchwork, Seurat plots |

---

## KEGG Pathways Investigated

`MAPK signalling` · `Ras signalling` · `Rap1 signalling` · `cGMP-PKG` · `HIF-1` · `PI3K-Akt` · `Apoptosis` · `VEGF signalling` · `Focal adhesion` · `Tight junction` · `Complement & coagulation` · `Collecting duct acid secretion` · `AGE-RAGE in diabetic complications` · `ECM-receptor interaction` · `Vascular smooth muscle contraction`

---

## Requirements

```r
library(Seurat)           # v5 — core scRNA-Seq analysis
library(SeuratObject)
library(sctransform)
library(harmony)          # Batch integration
library(uwot)             # UMAP
library(MAST)             # Differential expression
library(clusterProfiler)  # Pathway enrichment
library(org.Hs.eg.db)     # Gene ID mapping
library(pathview)         # KEGG pathway visualisation
library(ggplot2)
library(patchwork)
library(dplyr)
library(tidyr)
library(Matrix)
```

> Full session info: `environment/sessionInfo.txt`

---

## Data Availability

Raw data is not included in this repository. The dataset is a publicly available human intestinal scRNA-Seq resource accessed via the **Broad Single Cell Portal**.

---

## Author

**Aaliya**  
MSc Bioinformatics & Computational Biology — First Class Honours, University College Cork  
Graduate Research Assistant, APC Microbiome Ireland  
Research interests: AI for life sciences · scRNA-Seq · Multi-omics · Computational Biology

[![GitHub](https://img.shields.io/badge/GitHub-Aaliya09-181717?logo=github)](https://github.com/Aaliya09)

---

## Related Repositories

- [`Bioinformatics-ML-Portfolio`](#) — ALS/FTD RNA-Seq, breast cancer ML, QSAR modelling
- [`ML-Projects`](https://github.com/Aaliya09/ML-Projects) — Deep learning: image classification and NLP
## Pipeline Overview

The same core pipeline was applied across all datasets (with compartment-specific adaptations):
