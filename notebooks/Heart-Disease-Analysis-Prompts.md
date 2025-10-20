# Comprehensive LLM Prompts for Heart Disease Cleveland Dataset Analysis

## Dataset Information Summary
**Dataset:** Heart Disease Cleveland (UCI Machine Learning Repository)
**Source:** Cleveland Clinic Foundation  
**Records:** 303 patients  
**Features:** 14 clinical attributes  
**Target:** Heart disease presence (binary: 0=absence, 1=presence)  
**Download Sources:** 
- UCI: https://archive.ics.uci.edu/dataset/45/heart+disease
- Kaggle: https://www.kaggle.com/datasets/cherngs/heart-disease-cleveland-uci

---

## PROMPT 1: Loading the Dataset

```
I need to load and perform initial exploration of the Heart Disease Cleveland dataset for epidemiological analysis. This is a classic dataset from the Cleveland Clinic Foundation containing 303 patient records with 14 clinical attributes to predict heart disease presence.

Dataset characteristics:
- 303 patients from Cleveland Clinic
- 14 features: age, sex, cp (chest pain type), trestbps (resting blood pressure), chol (serum cholesterol), fbs (fasting blood sugar), restecg (resting ECG), thalach (max heart rate), exang (exercise angina), oldpeak (ST depression), slope (ST segment slope), ca (major vessels), thal (thalassemia), target (heart disease)
- Target variable: 0 = no heart disease, 1 = heart disease present
- Some missing values expected (particularly in ca and thal variables)

Please create Python code that:

1. **Loads the dataset** (provide multiple methods: direct download from UCI, Kaggle, or local CSV file)
2. **Displays basic dataset information:**
   - Dataset shape and size
   - Column names and data types
   - First and last 5 rows
   - Basic statistical summary (describe())
   - Memory usage information

3. **Performs initial data quality checks:**
   - Missing values count and percentage for each column
   - Duplicate records detection
   - Unique values count for each categorical variable
   - Data range verification for numerical variables

4. **Clinical context verification:**
   - Age range validation (should be realistic for adults)
   - Blood pressure ranges (trestbps should be 80-200 mmHg typically)
   - Cholesterol levels (chol should be 100-600 mg/dl typically)
   - Heart rate ranges (thalach should be 60-220 bpm typically)
   - Categorical variable value verification against expected ranges

5. **Target variable analysis:**
   - Distribution of heart disease cases (0 vs 1)
   - Percentage of positive cases
   - Class balance assessment

Please include all necessary imports (pandas, numpy, matplotlib, seaborn) and provide clear explanations for each step. The code should be ready to run in a Jupyter notebook environment.
```

---

## PROMPT 2: Reviewing and Preparing Data for Analysis

```
I have loaded the Heart Disease Cleveland dataset and now need to thoroughly review and prepare the data for epidemiological analysis. Based on the initial exploration, I need comprehensive data preparation focusing on clinical relevance and statistical validity.

Current dataset status:
- 303 patients with 14 clinical variables
- Target variable: heart disease presence (0/1)
- Missing values present in some variables (ca, thal primarily)
- Mixed data types (numerical and categorical)

Please create Python code for comprehensive data preparation:

1. **Missing Data Analysis:**
   - Create missing data patterns visualization (heatmap)
   - Analyze missing data mechanisms (MCAR, MAR, MNAR)
   - Calculate missing data percentage by variable
   - Assess if missing data is related to clinical outcomes
   - Implement appropriate missing data handling:
     * For ca (major vessels): Use median imputation or create "unknown" category
     * For thal (thalassemia): Use mode imputation or most frequent category
     * Justify chosen imputation method clinically

2. **Outlier Detection and Treatment:**
   - Use clinically appropriate outlier detection methods:
     * Age: flag if <18 or >100 years
     * trestbps: flag if <80 or >200 mmHg
     * chol: flag if <100 or >600 mg/dl
     * thalach: flag if <60 or >220 bpm
   - Create box plots and statistical outlier detection (IQR, Z-score)
   - Decide on outlier treatment (remove, cap, or keep with justification)
   - Document clinical reasoning for outlier decisions

3. **Variable Encoding and Transformation:**
   - Categorical variables proper encoding:
     * sex: already binary (0/1)
     * cp: chest pain type (ordinal: 0-3)
     * fbs: fasting blood sugar (binary: 0/1)
     * restecg: resting ECG (ordinal: 0-2)
     * exang: exercise angina (binary: 0/1)
     * slope: ST segment slope (ordinal: 1-3)
     * ca: major vessels (count: 0-3, handle missing)
     * thal: thalassemia (categorical: 3,6,7, handle missing)
   
   - Create meaningful category labels:
     * cp: 0='typical angina', 1='atypical angina', 2='non-anginal', 3='asymptomatic'
     * restecg: 0='normal', 1='ST-T abnormality', 2='LV hypertrophy'
     * slope: 1='upsloping', 2='flat', 3='downsloping'
     * thal: 3='normal', 6='fixed defect', 7='reversible defect'

4. **Feature Engineering:**
   - Create clinically meaningful derived variables:
     * Age groups: <45, 45-55, 55-65, >65 years
     * BP categories: normal (<120), elevated (120-129), stage 1 (130-139), stage 2 (≥140)
     * Cholesterol categories: optimal (<200), borderline (200-239), high (≥240)
     * Max HR percentage of predicted (220-age)
   
   - Create interaction variables if clinically relevant:
     * Age × Sex interaction
     * Chest pain × Exercise angina
     * Cholesterol × Age interaction

5. **Data Validation:**
   - Final data quality checks after preprocessing
   - Verify no impossible value combinations
   - Check correlation patterns for clinical sensibility
   - Create summary statistics by heart disease status
   - Generate data dictionary with variable descriptions

6. **Dataset Splitting:**
   - Create train/test split (80/20) stratified by target
   - Ensure balanced representation in both sets
   - Save processed datasets for analysis

Include detailed comments explaining clinical rationale for each preprocessing decision. Create visualizations to show before/after preprocessing effects.
```

---

## PROMPT 3: Formulating Research Hypotheses Based on Basic Statistics and Data Visualization

```
I have a cleaned and prepared Heart Disease Cleveland dataset (303 patients, 14 clinical variables). Now I need to conduct exploratory data analysis to formulate evidence-based research hypotheses for epidemiological investigation.

Dataset context:
- Cleaned dataset ready for analysis
- Target: heart disease presence (binary)
- 14 clinical predictors including demographics, symptoms, and test results
- Balanced analysis needed for hypothesis generation

Please create Python code that performs comprehensive exploratory analysis to generate research hypotheses:

1. **Univariate Analysis by Heart Disease Status:**
   - **Demographics:**
     * Age distribution: histograms, box plots, statistical tests (t-test/Mann-Whitney)
     * Sex distribution: cross-tabulation, chi-square test
     * Calculate mean age difference between diseased/healthy
     * Assess age-sex interaction patterns
   
   - **Clinical Symptoms:**
     * Chest pain types (cp) distribution by heart disease status
     * Exercise-induced angina (exang) prevalence comparison
     * Statistical significance testing for symptom-disease associations
   
   - **Clinical Measurements:**
     * Blood pressure (trestbps): distribution analysis, clinical cut-points
     * Cholesterol (chol): distribution analysis, clinical categories
     * Maximum heart rate (thalach): age-adjusted analysis
     * Fasting blood sugar (fbs) prevalence comparison
   
   - **Diagnostic Tests:**
     * Resting ECG (restecg) abnormalities by disease status
     * ST depression (oldpeak) patterns and clinical significance
     * ST segment slope (slope) distribution analysis
     * Major vessels (ca) involvement patterns
     * Thalassemia (thal) defect types by disease status

2. **Bivariate Analysis and Correlation:**
   - Create comprehensive correlation matrix for numerical variables
   - Cross-tabulation tables for categorical variables
   - Point-biserial correlations for categorical-numerical pairs
   - Identify strongest associations with heart disease
   - Clinical interpretation of correlation patterns

3. **Advanced Visualization for Hypothesis Generation:**
   - **Age-Sex stratified analysis:**
     * Heart disease prevalence by age groups and sex
     * Age-sex interaction heatmaps
     * Stacked bar charts showing disease patterns
   
   - **Risk Factor Combination Analysis:**
     * Multiple chest pain symptoms (cp + exang)
     * Blood pressure and cholesterol combined effects
     * Age with clinical measurements interactions
   
   - **Diagnostic Test Patterns:**
     * ECG abnormalities with ST depression correlation
     * Vessel involvement (ca) with other cardiac markers
     * Thalassemia types with disease severity indicators

4. **Statistical Evidence Summary for Hypothesis Formulation:**
   - Calculate effect sizes (Cohen's d, Cramer's V, odds ratios)
   - Identify variables with strongest associations (p<0.05, effect size >0.3)
   - Rank variables by predictive potential
   - Document clinical plausibility of observed associations

5. **Generate Formal Research Hypotheses:**
   Based on the exploratory analysis, formulate:
   
   **Primary Hypothesis:**
   - Main research question with strongest evidence
   - Specify direction and magnitude of expected effect
   
   **Secondary Hypotheses (3-4):**
   - Additional hypotheses supported by exploratory findings
   - Include interaction hypotheses if patterns suggest them
   
   **Each hypothesis should specify:**
   - Null hypothesis (H₀)
   - Alternative hypothesis (H₁)
   - Expected effect direction and magnitude
   - Clinical/biological rationale
   - Statistical test to be used for verification
   - Required assumptions for the test

6. **Create Evidence Summary Tables:**
   - Summary table of all associations found (variable, effect size, p-value, clinical interpretation)
   - Risk factor ranking by strength of association
   - Suggested analysis plan for hypothesis testing
   - Power analysis estimates for main hypotheses

Please ensure all analyses are clinically grounded and provide epidemiologically meaningful interpretations. Include detailed visualizations that support hypothesis formation and statistical evidence for each proposed hypothesis.
```

---

## PROMPT 4: Verifying Hypotheses Based on Statistical Tests

```
Based on my exploratory data analysis of the Heart Disease Cleveland dataset, I have formulated specific research hypotheses that need statistical verification. I need to conduct rigorous hypothesis testing using appropriate epidemiological methods.

Context from exploratory analysis:
- Dataset: 303 patients with heart disease status
- Generated specific hypotheses about risk factors
- Need formal statistical testing with appropriate methods
- Focus on clinical significance alongside statistical significance

Please create Python code for comprehensive hypothesis testing:

1. **Primary Hypothesis Testing:**
   [Note: Adapt based on your specific primary hypothesis from EDA]
   - **Example Primary Hypothesis:** "Age is significantly associated with heart disease risk"
   - **Statistical approach:**
     * Independent t-test or Mann-Whitney U test (depending on normality)
     * Test assumptions: normality (Shapiro-Wilk), equal variances (Levene's test)
     * Calculate effect size (Cohen's d)
     * 95% confidence intervals for mean differences
     * Clinical significance thresholds (e.g., >5 year mean difference)

2. **Secondary Hypotheses Testing:**
   
   **A. Categorical Risk Factors:**
   - **Sex and heart disease association:**
     * Chi-square test of independence
     * Fisher's exact test (if cell counts <5)
     * Odds ratio with 95% CI
     * Risk ratio and attributable risk calculations
   
   - **Chest pain types and heart disease:**
     * Chi-square test for trend (ordinal relationship)
     * Post-hoc pairwise comparisons with Bonferroni correction
     * Cramer's V for effect size
   
   - **Exercise angina and heart disease:**
     * Chi-square test, odds ratio calculation
     * Sensitivity, specificity, positive/negative predictive values

   **B. Continuous Risk Factors:**
   - **Blood pressure and heart disease:**
     * Independent t-test or Mann-Whitney U
     * Logistic regression for dose-response relationship
     * Clinical cut-point analysis (ROC curves)
   
   - **Cholesterol levels and heart disease:**
     * Statistical tests as above
     * Analysis using clinical categories (<200, 200-239, ≥240 mg/dl)
   
   - **Maximum heart rate and heart disease:**
     * Age-adjusted analysis using ANCOVA
     * Partial correlation controlling for age

3. **Multivariable Analysis:**
   - **Logistic Regression Model Building:**
     * Univariate screening (p<0.20 for inclusion)
     * Multicollinearity assessment (VIF <10)
     * Forward/backward stepwise selection
     * Model assumptions checking:
       - Linearity of logit for continuous variables
       - Independence of observations
       - Absence of influential outliers (leverage, Cook's distance)
   
   - **Model Performance:**
     * Hosmer-Lemeshow goodness-of-fit test
     * C-statistic (AUC) for discrimination
     * Classification metrics at optimal threshold
     * Cross-validation for internal validation

4. **Effect Modification and Interaction Analysis:**
   - **Age-Sex Interaction:**
     * Stratified analysis by sex
     * Logistic regression with interaction term
     * Likelihood ratio test for interaction significance
   
   - **Age-Risk Factor Interactions:**
     * Test interactions with main risk factors
     * Stratified analysis by age groups (<55, ≥55 years)
   
   - **Clinical Interpretation:**
     * Population attributable risk for modifiable factors
     * Number needed to treat/harm calculations where appropriate

5. **Multiple Comparisons Correction:**
   - Apply appropriate correction methods:
     * Bonferroni correction for family-wise error rate
     * False Discovery Rate (FDR) for exploratory analyses
     * Document corrected and uncorrected p-values
   - Justify correction method choice

6. **Power Analysis and Sample Size Adequacy:**
   - Post-hoc power analysis for non-significant findings
   - Calculate minimum detectable effect sizes
   - Assess if sample size adequate for observed effects
   - Clinical vs. statistical significance interpretation

7. **Sensitivity Analyses:**
   - **Missing Data Impact:**
     * Complete case analysis vs. imputed data comparison
     * Multiple imputation if substantial missing data
   
   - **Outlier Sensitivity:**
     * Analysis with and without extreme values
     * Robust statistical methods where appropriate
   
   - **Model Assumptions:**
     * Non-parametric alternatives for assumption violations
     * Bootstrap confidence intervals for robust inference

8. **Results Summary and Interpretation:**
   Create comprehensive results tables including:
   - **Univariate Results Table:**
     * Variable, test statistic, p-value, effect size, 95% CI
     * Clinical interpretation for each significant finding
   
   - **Multivariable Results Table:**
     * Adjusted odds ratios with 95% CI
     * Model performance metrics
     * Clinical significance assessment
   
   - **Hypothesis Testing Summary:**
     * Each hypothesis: H₀, test result, conclusion
     * Strength of evidence categorization
     * Clinical implications of findings

Please ensure all statistical tests are appropriate for the data types and research questions. Include assumption checking, effect size calculations, and clinical interpretation alongside statistical significance. Provide clear documentation of statistical methods used and their rationale.
```

---

## PROMPT 5: Analyzing Results

```
I have completed statistical hypothesis testing on the Heart Disease Cleveland dataset and now need comprehensive analysis and interpretation of results for epidemiological reporting and clinical application.

Context:
- Completed univariate and multivariable analyses
- Tested multiple hypotheses about heart disease risk factors
- Have statistical results including p-values, effect sizes, and confidence intervals
- Need clinical interpretation and public health implications

Please create Python code and framework for comprehensive results analysis:

1. **Statistical Results Synthesis:**
   
   **A. Evidence Strength Classification:**
   - Categorize findings by evidence strength:
     * Strong evidence: p<0.001, large effect size, biologically plausible
     * Moderate evidence: p<0.01, moderate effect size, clinically relevant
     * Weak evidence: p<0.05, small effect size, uncertain clinical relevance
     * Insufficient evidence: p≥0.05 or conflicting results
   
   **B. Effect Size Interpretation:**
   - Clinical significance thresholds for each variable:
     * Age: >5-year difference clinically meaningful
     * Blood pressure: >10 mmHg difference clinically meaningful
     * Cholesterol: >20 mg/dl difference clinically meaningful
     * Odds ratios: >2.0 or <0.5 clinically important
   
   - Create effect size visualization (forest plots)
   - Compare statistical vs. clinical significance

2. **Risk Factor Profile Analysis:**
   
   **A. Individual Risk Factors:**
   - **Demographic factors:**
     * Age: continuous relationship, optimal cut-points
     * Sex: risk differences and implications
   
   - **Modifiable risk factors:**
     * Blood pressure: dose-response relationship
     * Cholesterol levels: clinical categories analysis
     * Exercise capacity: protective vs. risk factors
   
   - **Clinical indicators:**
     * Chest pain patterns: diagnostic value
     * ECG abnormalities: prognostic significance
     * Exercise testing results: clinical utility
   
   **B. Risk Factor Combinations:**
   - High-risk profiles identification
   - Protective factor combinations
   - Risk stratification models

3. **Clinical Prediction Model Development:**
   
   **A. Final Model Selection:**
   - Compare different modeling approaches
   - Select optimal model based on:
     * Clinical interpretability
     * Statistical performance (AUC, calibration)
     * Parsimony (fewest variables for given performance)
   
   **B. Model Validation and Performance:**
   - Internal validation (bootstrap, cross-validation)
   - Calibration assessment (Hosmer-Lemeshow, calibration plots)
   - Discrimination assessment (ROC curves, sensitivity/specificity)
   - Clinical utility analysis (decision curve analysis)
   
   **C. Risk Score Development:**
   - Convert logistic regression to simple risk score
   - Create risk categories (low, moderate, high risk)
   - Validate risk categories with observed outcomes

4. **Population Health Implications:**
   
   **A. Attributable Risk Calculations:**
   - Population attributable risk for modifiable factors
   - Population attributable risk percentage
   - Number needed to treat/screen calculations
   - Years of life lost estimates (if mortality data available)
   
   **B. Public Health Impact:**
   - Prevalence of high-risk individuals
   - Potential preventable cases if risk factors modified
   - Cost-effectiveness considerations
   - Screening program implications

5. **Clinical Guidelines Comparison:**
   - Compare findings with established guidelines:
     * ACC/AHA cardiovascular risk guidelines
     * ESC/EAS dyslipidemia guidelines
     * JNC blood pressure guidelines
   
   - Identify concordance and discrepancies
   - Discuss implications for clinical practice

6. **Limitations and Bias Assessment:**
   
   **A. Study Limitations:**
   - **Selection bias:** Cleveland Clinic population representativeness
   - **Information bias:** measurement errors, recall bias
   - **Confounding:** unmeasured confounders discussion
   - **Temporal bias:** cross-sectional vs. longitudinal considerations
   
   **B. Statistical Limitations:**
   - Sample size limitations for subgroup analyses
   - Multiple testing considerations
   - Model overfitting assessment
   - Generalizability concerns

7. **Clinical Recommendations:**
   
   **A. Risk Assessment:**
   - Practical risk assessment tools
   - Clinical decision support recommendations
   - Patient counseling guidance
   
   **B. Preventive Interventions:**
   - Evidence-based intervention priorities
   - Lifestyle modification recommendations
   - Pharmacological intervention thresholds
   
   **C. Future Research:**
   - Knowledge gaps identified
   - Recommended study designs for unresolved questions
   - External validation needs

8. **Results Communication:**
   
   **A. Executive Summary:**
   - Key findings in 3-4 bullet points
   - Clinical bottom line
   - Public health implications
   
   **B. Technical Results Summary:**
   - Statistical results table with clinical interpretation
   - Model performance metrics
   - Risk stratification outcomes
   
   **C. Visual Results Summary:**
   - Key findings infographic
   - Risk factor importance ranking
   - Clinical decision flowchart

9. **Report Generation:**
   Create structured report sections:
   - **Methods Summary:** Brief statistical approach description
   - **Key Results:** Main findings with effect sizes and CI
   - **Clinical Interpretation:** What results mean for patient care
   - **Public Health Impact:** Population-level implications
   - **Limitations:** Study constraints and potential biases
   - **Conclusions:** Evidence-based recommendations
   - **Future Directions:** Research and implementation needs

Please ensure all analyses focus on practical clinical application and include appropriate cautions about study limitations. Provide clear distinction between statistical significance and clinical importance throughout the analysis.
```

---

## Usage Instructions

### For Each Prompt:
1. **Copy and paste** the entire prompt into your preferred LLM (ChatGPT, Claude, etc.)
2. **Run the generated code** in Jupyter Notebook
3. **Review and modify** code as needed for your specific dataset version
4. **Document your findings** from each step before proceeding to the next prompt

### Dataset Download Options:
- **UCI Direct:** Use the `ucimlrepo` package as shown in the first prompt
- **Kaggle:** Download from https://www.kaggle.com/datasets/cherngs/heart-disease-cleveland-uci
- **Local File:** Save as CSV and adjust file path in loading code

### Important Notes:
- **Verify data format:** Different sources may have slightly different variable names or encodings
- **Missing values:** Some versions have missing values coded as '?' instead of NaN
- **Target variable:** Ensure proper binary encoding (0/1) from original multi-class (0-4)
- **Clinical context:** Always validate statistical findings against medical knowledge

### Sequential Workflow:
These prompts are designed to be used sequentially, with each building on the previous analysis. Each prompt produces outputs that inform the next stage of analysis, creating a comprehensive epidemiological study workflow.

### Customization:
Feel free to modify the prompts based on:
- Your specific research questions
- Available computational resources
- Desired depth of analysis
- Target audience for results

This comprehensive prompt set provides a complete framework for conducting professional-level epidemiological analysis of the Heart Disease Cleveland dataset using LLM assistance.