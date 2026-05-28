# Customer Churn Optimization: End-to-End Exploratory Data Analysis (EDA)

[![Python Version](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Library-Pandas-orange.svg)](https://pandas.pydata.org/)
[![Seaborn](https://img.shields.io/badge/Library-Seaborn-green.svg)](https://seaborn.pydata.org/)

## 📈 Executive Summary & Business Impact
Customer attrition within subscription models represents a direct leak of annualized recurring revenue (ARR). This repository contains an end-to-end data auditing and exploratory pipeline executed on 7,043 subscriber records (IBM Telco Dataset). 

### Key Quantitative Findings:
* **Early Tenure Crisis:** 17.6% of all recorded accounts drop out within the **first 5 months** of activation.
* **The Contract Trap:** Month-to-Month contracts account for **88.5% of total company churn**, with an aggressive median dropout age of just ~7 months.
* **Pricing Elasticity Friction:** Multivariate modeling confirms a positive correlation (+0.19) between high monthly costs and customer exit rates, signaling price sensitivity across premium tiers.

---

## 🛠️ Data Pipeline & Architecture
The project is constructed chronologically across five operational phases designed to preserve structural pipeline integrity:

### Phase 1: Ingestion & Structural Audit
* Coerced `TotalCharges` from an uncomputable string object vector into a numeric floating-point decimal via `pd.to_numeric(..., errors='coerce')`.
* Isolated hidden data omissions (blank whitespace cells `' '`) and determined they correlated exclusively with brand-new accounts with a `tenure` of 0 months.
* Handled anomalies systematically by imputing missing values to `0.0`.

### Phase 2: Univariate Distribution Mapping
* Dissected distribution properties for continuous values (`tenure` and `MonthlyCharges`) leveraging Kernel Density Estimation (KDE) plot matrices.
* Revealed heavy **bimodal polarization** within customer lifespans, pinpointing two extreme user cohorts: immediate dropouts vs. ultra-loyal multivariable users.

### Phase 3: Bivariate & Multivariate Exploration
* Cross-examined categorical billing types against temporal metrics using grouped box plots split by target categories.
* Engineered a binary target variable (`Churn_Numeric`) to compute a clean Pearson correlation matrix, revealing linear dependency links between pricing models and retention lifespans.

---

## 📊 Visual Insights & Technical Inferences

### 1. Tenure & Monthly Charges Polarization
Continuous feature profiling shows extreme data density distributions. The customer base contains highly concentrated clusters at both poles of the timeline (months 1–5 and months 65–72). 
* **Insight:** The retention battle is determined in the initial lifecycle stage. If a subscriber crosses month 12 safely, their expected customer lifetime value multiplies exponentially.

### 2. Contractual Risk Grouping
Grouped box plots reveal that subscribers on Month-to-month terms who drop out exhibit a highly compressed, low-tenure lifespan with a median sitting comfortably under 8 months. 
* **Insight:** Formally transitioning subscribers to stable, long-term annual agreements completely flattens early attrition risk factors.

### 3. Pearson Metric Multipliers
The continuous feature heatmap identifies customer lifespan (`tenure`) as the primary continuous negative correlate to attrition (-0.35). Conversely, high monthly fees carry a positive correlation value (+0.19) to customer exit events, validating recurring cost friction.

---

## 💡 Data-Driven Strategic Recommendations

Based on the statistical shapes discovered during EDA, the business should implement two targeted operational adjustments:
1. **The Contract Migration Play:** Deploy automated promotional triggers targeting high-utilization Month-to-Month accounts between months 3 and 5, offering a targeted 10% loyalty credit if they switch to a 1-year contract tier.
2. **Premium Cohort Proactive Safety Net:** Establish automated customer success outreach workflows at Day 30 and Day 90 for any new subscriber carrying high monthly charges (exceeding \$80) to smooth installation issues before cost friction triggers.

---

## 💻 Tech Stack & Environment
* **Core Language:** Python 3.x
* **Data Engineering & Manipulation:** `pandas`, `numpy`
* **Data Visualization Matrix:** `matplotlib`, `seaborn`
* **Development Environment:** Jupyter Notebook Ecosystem

## 🚀 Repository Execution
To run the full exploratory notebook locally, configure your environment using the commands below:

```bash
# Clone the project repository
git clone [https://github.com/Rakesh311203/Telecom-Churn-EDA.git]

# Navigate into the project root directory
cd telecom-churn-eda

# Run Jupyter Notebook
jupyter notebook
