# Workforce Analytics & Retention Insights

> Exploratory People Analytics for Data-Informed Workforce Decisions

## Project Overview

This project demonstrates an end-to-end workforce analytics workflow
using a synthetic HR dataset. The goal is not to predict which
individual employee will leave, but to identify organizational patterns
associated with observed attrition and translate them into responsible,
evidence-informed workforce insights.

The analysis combines hypothesis-driven exploratory data analysis with
multivariate logistic regression, model evaluation under class
imbalance, and careful interpretation of associations and limitations.

## Business Question

**Which workforce characteristics are associated with employee
attrition, and how can workforce data support responsible,
evidence-informed retention analysis?**

The analysis focuses on workload and working conditions, business
travel, career development, job role, compensation, and employee
satisfaction.

## Dataset

The project uses the **IBM HR Analytics Employee Attrition &
Performance** dataset, a fictional workforce dataset created by IBM data
scientists and made publicly available through Kaggle.

-   **Records:** 1,470
-   **Variables:** 35
-   **Target:** `Attrition`
-   **Observed attrition:** 16.1%
-   **Non-attrition:** 83.9%
-   **Missing values:** none identified

The dataset includes employee demographics, job characteristics,
compensation, satisfaction, business travel, overtime, training, and
career-development variables.

**Source:** IBM HR Analytics Employee Attrition & Performance\
**Public dataset:**
https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset

Because the dataset is synthetic, the findings should not be interpreted
as evidence about a real organization.

## Analytical Approach

1.  Data structure and quality checks
2.  Hypothesis-driven exploratory data analysis
3.  Normalized group comparisons
4.  Analytical binning and income quartiles
5.  Correlation and stratified analysis
6.  Multivariate logistic regression
7.  Evaluation under class imbalance
8.  Confusion-matrix and classification-threshold analysis
9.  Coefficient and odds-ratio interpretation
10. Responsible business interpretation

## Key Findings

### Overtime

Employees working overtime show **30.5% observed attrition**, compared
with **10.4%** among employees without overtime.

In the multivariate model, overtime remains positively associated with
attrition (**OR = 4.10**).

### Business Travel

Observed attrition increases with travel frequency:

-   Non-Travel: **8.0%**
-   Travel Rarely: **15.0%**
-   Travel Frequently: **24.9%**

Frequent business travel also remains positively associated with
attrition in the multivariate model (**OR = 3.22** relative to
non-travellers).

### Job Role

Observed attrition differs substantially across job roles. **Sales
Representatives show the highest rate at 39.8%**.

The model also shows a strong positive association for Sales
Representatives relative to Healthcare Representatives (**OR = 5.80**).

These differences are descriptive and may reflect other role-related
characteristics such as workload, compensation, travel, or career
structure.

### Compensation and Workforce Structure

Employees in the lowest income quartile show **29.3% observed
attrition**.

However, `MonthlyIncome` and `JobLevel` are strongly related (**r =
0.95**), demonstrating why compensation should not be interpreted in
isolation.

A stratified comparison within Job Level 1 still shows higher attrition
in the lowest income quartile (**30.1%**) than in the lower-middle
quartile (**19.1%**).

### Satisfaction

Low job satisfaction is associated with **22.8% attrition**, compared
with **11.3%** for very high job satisfaction.

Low environment satisfaction shows **25.4% attrition**, compared with
**13.5%** for very high environment satisfaction.

### Hypotheses Not Fully Supported

Not every plausible workforce hypothesis was confirmed. Years since last
promotion shows no consistent increase in attrition, while work-life
balance and job level show non-linear patterns.

This is an important part of the analytical workflow: hypotheses are
tested rather than assumed to be true.

## Multivariate Model

A logistic regression model was selected because it supports transparent
interpretation of conditional associations.

The model includes:

-   Overtime
-   Business travel
-   Work-life balance
-   Training participation
-   Job role
-   Job satisfaction
-   Environment satisfaction
-   Monthly income
-   Years since last promotion

`JobLevel` was not included alongside `MonthlyIncome` because the two
variables are very strongly correlated in this dataset.

Categorical predictors are one-hot encoded and numerical predictors are
standardized within a scikit-learn pipeline. The train-test split is
stratified to preserve the imbalanced target distribution.

## Model Evaluation

Test-set performance:

  Metric                       Result
  ------------------------- ---------
  Accuracy                      86.7%
  Precision                     83.3%
  Recall                        21.3%
  F1-score                      33.9%
  ROC-AUC                       76.8%
  Naive accuracy baseline     \~84.0%

The model achieves only a small accuracy improvement over a naive
majority-class baseline. More importantly, recall for observed attrition
is low at the default threshold.

The ROC-AUC of **0.768** indicates meaningful but imperfect
discrimination across thresholds.

A threshold analysis is included to demonstrate the precision-recall
trade-off, not to recommend an operational employee-level classification
threshold.

## Business Implications

The results suggest several areas for organizational investigation:

-   Review sustained overtime patterns across teams and roles.
-   Examine the organizational impact of frequent business travel.
-   Investigate working conditions in roles with comparatively high
    observed attrition.
-   Review compensation together with job level and career structure.
-   Explore the organizational context behind low job and environment
    satisfaction.
-   Combine quantitative analysis with employee feedback, interviews,
    and organizational context before designing retention initiatives.

## Responsible Use & Limitations

This project is designed as **decision support at an organizational
level**, not as an employee-scoring system.

Key limitations:

-   Associations do not establish causality.
-   The synthetic dataset may not represent the complexity of real
    organizations or labour markets.
-   Several workforce characteristics overlap strongly.
-   Model performance is moderate, with low recall for the minority
    attrition class at the default threshold.
-   Odds ratios describe associations within this specific fitted model
    and dataset, not universal effects.
-   Individual attrition predictions could create fairness, privacy, and
    discrimination risks if used operationally.

The model should **not** be used to label employees as "flight risks",
automate employment decisions, or determine access to opportunities.

## Tech Stack

-   **Python**
-   **pandas**
-   **NumPy**
-   **Matplotlib**
-   **scikit-learn**
-   **Google Colab**

Methods include exploratory data analysis, cross-tabulation,
segmentation, correlation analysis, stratified comparison, logistic
regression, ROC-AUC evaluation, confusion-matrix analysis, and
classification-threshold analysis.

## Repository Structure

``` text
workforce-analytics-retention/
├── README.md
└── Workforce_Analytics_&_Retention_Insights.ipynb
```

The dataset is not required to be stored in the repository. It can be
downloaded from the public Kaggle source linked above.

## How to Run

1.  Download the IBM HR Analytics Employee Attrition & Performance CSV
    from Kaggle.
2.  Open the notebook in Google Colab or Jupyter.
3.  Upload `WA_Fn-UseC_-HR-Employee-Attrition.csv` when prompted.
4.  Run the notebook from top to bottom.

## Conclusion

The project demonstrates a complete analytical workflow from
business-oriented hypothesis formulation and data-quality checks to
exploratory analysis, multivariate modelling, model evaluation, and
responsible interpretation.

The central takeaway is that the value of people analytics is not simply
to predict who may leave, but to identify organizational patterns that
can guide deeper investigation and better-informed workforce decisions.
