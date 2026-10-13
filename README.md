# Missing Data Imputation in Prostate Cancer Registry Data

**Evaluating Statistical and Machine Learning Approaches Under Different Missingness Mechanisms**

### MS Capstone Research | Public Health Data Science

**Research areas:** Biostatistics · Cancer Epidemiology · Missing Data · Machine Learning · Spatial Statistics · Health Data Science

## Project Overview

Missing data are a persistent challenge in cancer registry research. Incomplete clinical information can affect statistical estimates, predictive modeling, and the reliability of epidemiological findings.

Tumor grade is an important clinical characteristic in prostate cancer research because it provides information about disease aggressiveness and can inform clinical risk assessment.

This capstone project investigated how different statistical and machine learning approaches perform when imputing missing tumor grade values in a large prostate cancer registry dataset.

The analysis included **41,545 patient records and 396 original variables**, with approximately **28.1% of tumor grade observations missing**.

Rather than assuming all missing values occurred randomly, the project examined different missingness mechanisms and compared imputation methods based on predictive performance, uncertainty, and preservation of data characteristics.

The central research question was:

**Which imputation approaches provide reliable estimates of missing tumor grade while accounting for different missingness mechanisms and preserving clinically and geographically meaningful patterns?**

## Research Objectives

1. Examine the extent and patterns of missing tumor grade information in prostate cancer registry data.
2. Investigate whether missingness is associated with patient demographics and geographic characteristics.
3. Simulate missing values under different missing-data mechanisms.
4. Compare conventional statistical imputation with machine learning-based approaches.
5. Evaluate imputation accuracy, uncertainty, and distributional characteristics.
6. Examine the potential value of geographically stratified imputation.

## Dataset Description

The project used prostate cancer registry data containing patient-level demographic, clinical, and geographic information.

| Characteristic | Description |
|---|---|
| Study population | 41,545 prostate cancer records |
| Original variables | 396 |
| Primary imputation target | Tumor grade |
| Missing tumor grade | Approximately 28.1% |
| Analysis | Statistical and machine learning imputation |
| Software | Python and R |

A reduced analytical dataset of selected variables was developed for modeling and evaluation.

**Data confidentiality:** The original patient-level registry dataset is not included in this public repository. Access and redistribution are subject to the source registry's applicable data-use and confidentiality requirements.

## Missing Data Assessment

The initial analysis examined patterns of missing tumor grade values and relationships between missingness and available patient characteristics.

Age and race were significantly associated with missing tumor grade information (p < 0.001), suggesting that the observed missingness pattern was inconsistent with a simple completely random missingness assumption.

Spatial analysis also identified a small but statistically significant geographic clustering signal:

- Moran's I = 0.013
- p = 0.001

These findings motivated a comparison of imputation approaches under alternative missingness assumptions.

## Missingness Mechanisms

The project considered three principal mechanisms.

### 1. Missing Completely at Random (MCAR)

Values are missing independently of observed and unobserved characteristics.

### 2. Missing at Random (MAR)

The probability of missingness depends on observed variables, such as demographic or clinical characteristics.

### 3. Missing Not at Random (MNAR)

The probability of missingness may depend on unobserved values or other processes not fully explained by observed variables.

The simulation framework included **15 missingness scenarios**, representing three missingness mechanisms across five simulated missingness levels.

The MNAR scenarios were treated as sensitivity assumptions rather than proof that the registry's missing values followed an identifiable MNAR mechanism.

## Imputation Methods

Four methodological approaches were investigated.

### Method 1: Iterative Imputation

A chained-equation-style iterative imputation approach implemented using Python's `IterativeImputer`, including posterior sampling.

**Purpose:** Establish a conventional iterative imputation benchmark.

### Method 2: miceforest

A machine learning-based chained-equation approach using tree-based predictive models.

**Purpose:** Explore flexible nonlinear imputation.

**Implementation note:** The attempted implementation encountered software compatibility and data-encoding problems. It should not be interpreted as a successfully validated benchmark.

### Method 3: SuperMICE-Style Balanced Random Forest

A random forest-based imputation approach incorporating class-balancing strategies to address the distribution of tumor grade categories.

**Purpose:** Improve patient-level categorical imputation performance while retaining meaningful variability across imputations.

### Method 4: Geographically Stratified Random Forest

A random forest-based imputation approach that considers geographic strata during model development.

**Purpose:** Investigate whether accounting for geographic heterogeneity improves the preservation of local data patterns.

## Analytical Workflow

### Phase 1: Data Preparation

- Examine variable completeness and missingness.
- Recode tumor grade values representing unknown categories as missing.
- Select demographic, clinical, and geographic predictors.
- Prepare analytical datasets.
- Examine distributions and potential predictors of missingness.

### Phase 2: Missingness Simulation

- Generate artificial missingness under MCAR, MAR, and MNAR assumptions.
- Apply multiple missingness levels.
- Retain known values for evaluating imputation accuracy.
- Construct comparable evaluation scenarios.

### Phase 3: Imputation Modeling

- Fit iterative imputation models.
- Evaluate tree-based imputation approaches.
- Apply balanced random forest methods.
- Investigate geographically stratified models.

### Phase 4: Model Evaluation

The evaluation considered:

**Predictive performance**
- Accuracy of imputed tumor grade categories
- Macro-averaged F1 score
- Performance across different missingness scenarios

**Statistical uncertainty**
- Between-imputation variability
- Fraction of missing information (λ), where applicable
- Stability of imputed estimates

**Distributional and geographic characteristics**
- Preservation of tumor grade distributions
- Geographic heterogeneity
- Potential effects of imputation on epidemiological interpretation

## Key Findings

### 1. Missingness was not consistent with MCAR

Tumor grade missingness was associated with patient characteristics, including age and race.

This demonstrates why missing-data diagnostics should precede the selection of an imputation method.

### 2. Balanced random forest showed stronger patient-level performance

The SuperMICE-style balanced random forest approach achieved macro-F1 scores of approximately **0.265–0.316** across the evaluated scenarios.

It also produced nonzero measures of imputation uncertainty, with reported λ values ranging from approximately 0.51 to 0.87.

Although these results were stronger than the successfully evaluated alternatives, the modest macro-F1 scores indicate that accurate prediction of individual tumor grades remained challenging.

### 3. Geographic stratification provided an alternative approach

The geographically stratified random forest method preserved meaningful geographic and distributional characteristics in the evaluated analyses.

Reported λ values ranged approximately from 0.40 to 0.79.

These findings suggest that geographic information may be useful when developing imputation strategies for spatially structured registry data.

### 4. Implementation success did not guarantee valid multiple imputation

The iterative imputation implementation ran, but its reported uncertainty diagnostics included λ = 0, raising concerns about whether the implementation adequately represented between-imputation uncertainty.

The `miceforest` implementation was not successfully completed because of compatibility and encoding issues.

These limitations are important when interpreting comparisons among the four methods.

### 5. Missing-data mechanisms matter

The analysis demonstrated that imputation performance and uncertainty can differ depending on the assumed missingness process.

No imputation method can establish the true values of missing observations without additional assumptions or external validation.

## Tools and Technologies

**Programming:** Python and R

**Python tools:**
- pandas
- NumPy
- scikit-learn
- IterativeImputer
- Random Forest

**R and statistical analysis:**
- Missing-data diagnostics
- Statistical summaries
- Spatial autocorrelation analysis
- Data visualization
- Model evaluation

**Core competencies demonstrated:**

- Healthcare data preprocessing
- Missing-data simulation
- Statistical imputation
- Machine learning for categorical outcomes
- Model validation
- Spatial epidemiology
- Reproducible analytical research

## Limitations

Several limitations should be considered when interpreting the results.

First, simulated missingness mechanisms provide controlled evaluation conditions but may not fully reproduce the actual missingness process in cancer registry data.

Second, the modest predictive performance of the strongest evaluated approach indicates uncertainty in patient-level tumor grade classification.

Third, not all proposed imputation methods were successfully implemented and validated.

Fourth, geographic stratification may preserve local data characteristics but does not necessarily eliminate selection bias or unmeasured confounding.

Finally, conclusions from this registry should not automatically be generalized to other cancer registries or clinical populations.

## Research Significance

This project illustrates the importance of moving beyond simple missing-value replacement toward systematic evaluation of imputation assumptions, predictive performance, and statistical uncertainty.

Its broader applications include:

- Cancer registry data quality
- Clinical and epidemiological research
- Electronic health record analytics
- Missing-data methodology
- Machine learning in healthcare
- Geographic health disparities research

The central lesson is that **a good imputation method should not be judged solely by predictive accuracy; it should also be evaluated for uncertainty, distributional preservation, and compatibility with the scientific question.**

## Reproducibility

The repository is intended to document the analytical workflow, model implementations, evaluation procedures, and selected non-identifiable results.

Reproducibility materials may include:

- Data preparation scripts
- Missingness simulation code
- Imputation model implementations
- Model evaluation scripts
- Figures and summary tables
- Documentation of software requirements

The original patient-level data will not be redistributed unless expressly permitted by the data provider.

Researchers with authorized access to the underlying data can adapt the documented workflow to reproduce or extend the analysis.

## Author

**Md Saiful Hasan, MS**  
Public Health Data Science  
College of Public Health  
Temple University  
Philadelphia, Pennsylvania, USA

**Research interests:** Biostatistics, Epidemiology, Machine Learning, Health Informatics, Missing Data, and Spatial Data Science.

## Citation

If you use the methods or code from this project, please acknowledge the author and cite any associated publication when available.

**Project:** *Missing Data Imputation in Prostate Cancer Registry Data: A Comparative Evaluation of Statistical and Machine Learning Approaches.*

**Academic context:** Master of Science Capstone Research, Temple University.

## License

A license for original code and documentation will be specified separately. The underlying patient-level registry data are not covered by any repository code license.
