# 🧬 AHBA Alzheimer's Risk Gene Expression Analysis

[![Python](https://img.shields.io/badge/Python-3.12-blue.svg)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-2.0+-green.svg)](https://pandas.pydata.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 📊 Overview

This repository contains a neurogenomics analysis of **Allen Human Brain Atlas (AHBA)** microarray data to investigate the regional expression patterns of **Alzheimer's disease (AD) risk genes** across the human cortex.

**Key Finding:** CD33, an immune receptor on microglia, shows the strongest upregulation in AD-vulnerable brain regions (Log2FC = 0.78, q = 0.006).

---

## 🔬 Key Results

### Differential Expression Analysis (6 Donors)

After FDR correction (Benjamini-Hochberg, q < 0.05), **4 genes** showed robust upregulation in AD-vulnerable regions:

| Gene | Log2FC | Fold Change | q-value | Role |
|------|--------|-------------|---------|------|
| **CD33** | **0.78** | **1.72x ↑** | **0.006** | Immune receptor (microglia) |
| **APOE** | **0.60** | **1.52x ↑** | **0.006** | Lipid metabolism, amyloid clearance |
| **FERMT2** | **0.58** | **1.49x ↑** | **0.006** | Cell adhesion, actin binding |
| **BIN1** | **0.55** | **1.46x ↑** | **0.007** | Endocytosis, tau pathology |

### PCA (3 Donors - Exploratory)

PCA was performed on 3 donors due to memory constraints. PC1 explained 92.52% of variance, which is **consistent with technical artifacts** (batch effects, donor heterogeneity). This PCA is **not biologically interpretable** and is included as a secondary, exploratory visualization.

| Component | Variance Explained | Interpretation |
|-----------|-------------------|----------------|
| PC1 | 92.52% | Technical artifact |
| PC2 | 1.24% | Noise |
| PC1-5 | 95.35% | Almost all variation captured |

**Conclusion:** The PCA is not biologically interpretable. All biological conclusions are based on the **FDR-corrected differential expression analysis** from 6 donors.

---

## 🛠️ Methods

### Data Source
- **Allen Human Brain Atlas (AHBA)**: Microarray expression data
- **Donors**: 6 donors (10021, 9861, 12876, 15496, 15697, 14380)
- **Atlas**: Desikan-Killiany parcellation (68 cortical regions)

### Analysis Pipeline

1. **Data Processing**
   - Used `abagen` Python library to extract and normalize expression data
   - Probe selection: `max_variance` (single donor compatible)
   - Normalization: Scaled robust sigmoid (SRS)

2. **Gene Selection**
   - Focused on 12 AD risk genes from Kunkle et al. (2019) GWAS
   - Genes: APOE, BIN1, CLU, CR1, PICALM, MS4A6A, CD33, ABCA7, TREM2, SORL1, ADAM10, FERMT2, HLA-DRB1, INPP5D

3. **Region Classification**
   - **AD-vulnerable regions**: Hippocampus, entorhinal cortex, parahippocampal gyrus, posterior cingulate, isthmus cingulate
   - **Control regions**: Precentral gyrus, postcentral gyrus, pericalcarine cortex, cuneus

4. **Statistical Analysis**
   - Independent t-test (unequal variance, Welch's correction)
   - Effect size: Log2 fold change
   - Multiple testing correction: FDR (Benjamini-Hochberg, q < 0.05)
   - Significance threshold: q < 0.05 and |Log2FC| > 0.1

5. **PCA (Exploratory)**
   - Performed on 3 donors due to memory constraints
   - Not biologically interpretable (PC1 = 92.52% technical artifact)
   - Included as secondary visualization only

### Dependencies

```bash
pip install -r requirements.txt
