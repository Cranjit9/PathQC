# GTEx Whole-Slide Image Analysis Pipeline

## Overview

This pipeline analyzes GTEx (Genotype-Tissue Expression) whole-slide histological image features to predict tissue quality metrics. The primary goal is to build predictive models that can estimate RNA integrity (RIN scores) and tissue degradation levels (autolysis scores) from extracted image features across different human tissue types.

## What We're Predicting

### Primary Targets
- **RIN Scores (RNA Integrity Number)**: Predicts RNA quality on a scale of 1-10, where higher scores indicate better preserved RNA
- **Autolysis Scores**: Predicts tissue degradation levels (0=none, 1=mild, 2=moderate, 3=severe)

### Why This Matters
- **Quality Control**: Automated assessment of tissue sample quality before expensive downstream analysis
- **Resource Optimization**: Prioritize high-quality samples for RNA sequencing and other molecular assays
- **Tissue Banking**: Improve sample selection and storage protocols
- **Research Impact**: Enable better quality-aware analysis of GTEx data

## Methodology

### Data Integration
- Combines H5-formatted image features with GTEx metadata
- Integrates quality metrics (RIN, autolysis) with demographic information
- Processes 30+ tissue types with thousands of samples

### Analysis Pipeline
1. **Feature Processing**: Standardization and quality filtering of image-derived features
2. **Exploratory Analysis**: Tissue distribution, quality score patterns, demographic effects
3. **Dimensionality Reduction**: PCA and UMAP for tissue clustering visualization
4. **Predictive Modeling**: Tissue-specific Lasso regression with cross-validation
5. **Model Evaluation**: Performance assessment, stability analysis, feature importance

### Key Innovations
- **Tissue-specific models**: Individual predictive models for each tissue type
- **Feature selection**: Correlation-based selection of top 5% most predictive features
- **Cross-validation**: 5-fold CV ensures robust performance estimates
- **Comprehensive evaluation**: Multiple metrics (R, RMSE, MAE) and stability assessment

## Quick Start

### Installation
```r
# Core packages
install.packages(c(
  "tidyverse", "data.table", "ggplot2", "readxl",
  "umap", "glmnet", "caret", "corrplot"
))

# Bioconductor for HDF5 support
BiocManager::install("rhdf5")
```

### Data Structure
```
PathQC/
├── data/raw/
│   ├── GTEX_AGGREGATED/concatnated_features_pooled.h5
│   └── metadata/ (GTEx annotation files)
├── src/ (analysis scripts)
└── output/ (generated figures and results)
```

### Usage
```r
# Set base directory
base_dir <- "/path/to/PathQC"

# Run main analysis
source("gtex_analysis_pipeline.R")

# Run predictive modeling
source("gtex_tissue_modeling.R")
```

## Technical Details

### System Requirements
- **R**: Version 4.0 or higher
- **Memory**: 8GB RAM minimum, 16GB recommended
- **Runtime**: 1-2 hours for complete analysis
- **Dependencies**: See installation section

### Model Specifications
- **Algorithm**: Lasso regression with L1 regularization
- **Feature selection**: Top 5% by correlation with target variable
- **Cross-validation**: 5-fold stratified CV
- **Performance metrics**: Pearson correlation (R), RMSE, MAE
- **Stability assessment**: Coefficient of variation across folds

## Applications

### Research Applications
- Quality-aware analysis of GTEx expression data
- Tissue-specific quality control protocols
- Histological image analysis method development

### Clinical Potential
- Automated tissue quality assessment
- Sample prioritization for expensive assays
- Quality control in biobanking operations

## Contributing

We welcome contributions! Please see our contributing guidelines for:
- Code style requirements
- Testing procedures
- Documentation standards
- Issue reporting

---

**Note**: This pipeline is designed for research purposes. Ensure compliance with GTEx data use agreements and institutional policies.
