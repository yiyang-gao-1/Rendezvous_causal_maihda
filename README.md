# 🔬 Causal-MAIHDA Analysis Pipeline

## 📋 Overview

This repository provides a comprehensive R analysis pipeline for conducting MAIHDA (Multilevel Analysis of Individual Heterogeneity and Discriminatory Accuracy) with causal extensions on the ACIC 2022 Track 1 competition data. The pipeline demonstrates both conventional MAIHDA approaches and novel causal-MAIHDA methodologies, bridging descriptive intersectional analysis with causal inference.

## 📁 Repository Contents

### 🎯 Core Analysis Scripts

1. **`01_data_structure_merge.Rmd`**: Data preparation and merging guide 🔧
   - Explains the ACIC 2022 Track 1 four-file structure
   - Provides merge rules for patient, practice, and temporal data
   - Creates human-readable intersectional strata from abstract variables
   - Assigns teaching-friendly semantics to all variables

2. **`02_conventional_maihda.Rmd`**: Traditional MAIHDA implementation 📊
   - Constructs intersectional strata from patient characteristics
   - Calculates Variance Partition Coefficients (VPC) and Proportional Change in Variance (PCV)
   - Fits multilevel models with random intercepts and slopes
   - Generates caterpillar plots for visualising stratum-specific effects
   - Quantifies treatment effect heterogeneity across strata

3. **`03_causal_maihda.Rmd`**: Causal-MAIHDA extensions 🎲
   - Implements intention-to-treat (ITT) average treatment effect estimation
   - Applies cluster-robust standard errors for practice-level randomisation
   - Extends MAIHDA with random slopes for treatment heterogeneity
   - Integrates causal forest for conditional average treatment effects (CATE)
   - Includes robustness checks via randomisation inference

4. **`04_high_vpc_finder.Rmd`**: Efficient VPC screening tool 🔍
   - Two-stage approach for identifying high-VPC replicates
   - Stage A: Fast proxy calculation using ANOVA decomposition
   - Stage B: Precise VPC estimation via mixed models for candidates
   - Optimised for screening large numbers of replicates

## 📊 Data Requirements

The scripts work with ACIC 2022 Track 1 data, which consists of four CSV files per replicate:
- `patient_xxxx.csv`: Time-invariant patient characteristics
- `patient_year_xxxx.csv`: Patient-year outcomes
- `practice_xxxx.csv`: Time-invariant practice characteristics  
- `practice_year_xxxx.csv`: Practice-year treatment assignments and aggregates

## 💻 Installation

### 📦 Required R Packages

```r
# Core packages
install.packages(c("dplyr", "tidyr", "readr", "data.table", "forcats", "stringr", "glue"))

# Modelling packages
install.packages(c("lme4", "fixest", "grf", "broom.mixed"))

# Visualisation
install.packages(c("ggplot2", "knitr"))

# Additional for robust inference
install.packages("clubSandwich")
```

## 🚀 Usage

### Step 1: Data Preparation 📥
Update the `data_dir` parameter in `01_data_structure_merge.Rmd` to point to your ACIC data folder, then run the script to understand the data structure and create the merged analysis dataset.

### Step 2: Conventional MAIHDA 📈
Run `02_conventional_maihda.Rmd` to perform traditional MAIHDA analysis. This will:
- Create intersectional strata based on patient characteristics
- Calculate VPC to quantify between-stratum heterogeneity
- Fit multilevel models and assess treatment effect variation

### Step 3: Causal Extensions (Optional) ⚡
For causal inference extensions, run `03_causal_maihda.Rmd`. Ensure you have saved the merged dataset from Step 2 (the script saves it as `causal_acic.csv`).

### Step 4: Finding High-VPC Replicates (Optional) 🎯
To identify replicates with substantial intersectional heterogeneity suitable for teaching or demonstration, use `04_high_vpc_finder.Rmd`.

## 🔑 Key Methodological Features

### 📐 Conventional MAIHDA
- Multilevel modelling with crossed random effects for practices and patients
- Intersectional strata formation from multiple social categories
- Variance decomposition to quantify discriminatory accuracy
- Random slope models for treatment effect heterogeneity

### 🎲 Causal-MAIHDA Extensions
- Integration of causal inference methods with MAIHDA framework
- Cluster-aware causal forest for heterogeneous treatment effects
- Practice-level randomisation with appropriate clustering adjustments
- Combination of design-based and model-based inference

## 📊 Output Interpretation

The analyses produce:
- **VPC**: Proportion of outcome variance attributable to intersectional strata
- **PCV**: Reduction in between-stratum variance after adjusting for main effects
- **ATE**: Average treatment effect with cluster-robust confidence intervals
- **CATE**: Conditional average treatment effects for subgroups
- **Treatment heterogeneity**: Standard deviation of random treatment slopes

## 📚 Citation

If you use this code in your research, please cite:
- The original MAIHDA methodology papers (Evans et al., 2018; Merlo, 2018)
- The ACIC 2022 competition for providing the data structure

## 📝 Notes

- The scripts assume ACIC 2022 Track 1 data structure
- Modify file paths in the parameter sections to match your directory structure
- Some analyses may take considerable time for large datasets; consider using the high-VPC finder to select representative replicates first

## 📄 License

This code is provided for educational and research purposes. Please check the ACIC competition terms for data usage restrictions.

## 📧 Contact

For questions or contributions, please open an issue on GitHub.
