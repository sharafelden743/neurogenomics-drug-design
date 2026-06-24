# 🧬 AHBA Alzheimer's Risk Gene Expression Analysis

[![Python](https://img.shields.io/badge/Python-3.12-blue.svg)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-2.0+-green.svg)](https://pandas.pydata.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR_USERNAME/neurogenomics-drug-design/blob/main/ahba_analysis.ipynb)

## 📊 Overview

This repository contains the complete analysis of **Allen Human Brain Atlas (AHBA)** microarray expression data to investigate the regional expression patterns of **Alzheimer's disease (AD) risk genes** across the human cortex.

### 🔬 Key Finding

**APOE**, the strongest genetic risk factor for late-onset Alzheimer's disease, shows **~3.1x higher expression** (Log2_FC = 1.636, p = 0.00012) in AD-vulnerable brain regions (hippocampus, entorhinal cortex, parahippocampal gyrus) compared to control regions (primary sensory and motor areas).

### 📈 Complete Results

| Gene | Log2_FC | Fold Change | P-Value | Significant |
|------|---------|-------------|---------|-------------|
| **APOE** | **+1.636** | **3.10x ↑** | **0.00012** | ✅ |
| **BIN1** | +0.898 | 1.86x ↑ | 0.0019 | ✅ |
| **CD33** | +0.743 | 1.67x ↑ | 0.00053 | ✅ |
| **TREM2** | +0.450 | 1.37x ↑ | 0.028 | ✅ |
| PICALM | +0.428 | 1.34x ↑ | 0.079 | ❌ |
| CLU | +0.306 | 1.24x ↑ | 0.122 | ❌ |
| **SORL1** | -0.309 | 1.24x ↓ | **0.00052** | ✅ |
| **ABCA7** | -0.315 | 1.24x ↓ | **0.034** | ✅ |

### 📊 Visualization

![Gene Expression Barplot](figures/gene_expression_barplot.png)

*Figure 1: Log2 fold change of AD risk genes in vulnerable vs. control brain regions. Red bars indicate upregulation in AD regions; blue bars indicate downregulation.*

## 🛠️ Methods

### Data Source
- **Allen Human Brain Atlas (AHBA)** : Microarray expression data from donor 10021
- **Atlas**: Desikan-Killiany parcellation (68 cortical regions)
- **Regions**: 83 cortical regions (including subcortical structures)

### Analysis Pipeline

1. **Data Processing**
   - Used `abagen` Python library to extract and normalize expression data
   - Probe selection: `max_expression` (single donor compatible)
   - Normalization: Scaled robust sigmoid (SRS)

2. **Gene Selection**
   - Focused on 10 AD risk genes from Kunkle et al. (2019) GWAS
   - Genes: APOE, BIN1, CLU, CR1, PICALM, MS4A6A, CD33, ABCA7, TREM2, SORL1

3. **Region Classification**
   - **AD-vulnerable regions**: Hippocampus, entorhinal cortex, parahippocampal gyrus, posterior cingulate, isthmus cingulate
   - **Control regions**: Precentral gyrus, postcentral gyrus, pericalcarine cortex, cuneus

4. **Statistical Analysis**
   - Independent t-test (unequal variance, Welch's correction)
   - Effect size: Log2 fold change
   - Significance threshold: p < 0.05

### Dependencies

```bash
pip install -r requirements.txt
