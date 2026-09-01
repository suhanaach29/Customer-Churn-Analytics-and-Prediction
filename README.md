# Customer Churn Analytics & Prediction

## Overview

Customer churn can have a significant impact on recurring revenue and long-term customer value. This project develops an end-to-end analytics and machine learning solution to understand customer churn, quantify its financial impact, identify high-risk customer segments, and support targeted retention strategies.

The project analyses **51,047 customer records** using Python, SQL, Power BI and machine learning. It combines descriptive analytics, customer segmentation, revenue analysis and predictive modelling to translate customer data into actionable business insights.

---

## Business Objectives

The analysis was designed to answer six key questions:

1. What is the overall customer churn rate?
2. Which customer segments demonstrate higher churn risk?
3. Which behavioural and customer characteristics are associated with churn?
4. How much monthly and annual revenue is associated with churn?
5. Which active customers should be prioritised for retention?
6. Can machine learning help identify customers more likely to churn?

---

## Tools & Technologies

- **Python** — Data cleaning, validation, exploratory analysis, feature engineering and machine learning
- **SQL / DuckDB** — Customer segmentation and analytical queries
- **Power BI** — Interactive dashboard development and business reporting
- **DAX** — KPI and business metric calculations
- **Pandas & NumPy** — Data manipulation and analysis
- **Scikit-learn** — Preprocessing and machine learning
- **XGBoost** — Churn prediction
- **Matplotlib** — Exploratory visualisation
- **Joblib** — Model pipeline persistence

---

## Dataset

The project uses the IBM Cell2Cell customer churn dataset containing customer demographic, account, usage, service and behavioural information.

After data preparation, the analysis covers:

- **51,047 customers**
- **14,711 churned customers**
- **36,336 retained customers**
- **28.8% overall churn rate**

---

## Data Preparation

The dataset was assessed and prepared before analysis and modelling.

Key steps included:

- Data type validation
- Missing-value analysis
- Duplicate checks
- Categorical consistency checks
- Feature validation
- Data transformation
- Feature engineering
- Model leakage prevention

Engineered analytical features included:

- Tenure Group
- Usage Trend
- Care Call Group
- Device Age Group
- Revenue Band
- Overage Band
- Estimated Lifetime Revenue
- Frustration Score
- Retention Priority
- Risk Score

---

## Key Business KPIs

| KPI | Result |
|---|---:|
| Total Customers | 51,047 |
| Churned Customers | 14,711 |
| Churn Rate | 28.8% |
| Monthly Revenue Associated with Churn | $852,498 |
| Annualised Revenue Associated with Churn | ~$10.23M |
| Active High-Priority Customers | 4,771 |
| Average Risk Score | 2.98 |

---

## Key Insights

### 1. Customer churn represents significant revenue exposure

Approximately **28.8% of customers churned**, representing approximately **$852K in monthly revenue** and an annualised revenue impact of approximately **$10.23M**.

### 2. Device age shows a strong churn pattern

Customers with devices **over two years old recorded approximately 36.1% churn**, compared with approximately **22.9% for customers with devices under six months old**.

This suggests device lifecycle is an important characteristic to consider when designing retention strategies.

### 3. Overage behaviour is associated with higher churn

Customers in the **very-high overage segment recorded approximately 31.7% churn**, compared with **27.1% among low-overage customers**.

### 4. Customer-care behaviour is not linear

Customers with **no customer-care calls recorded approximately 30.7% churn**, while customers with higher call volumes did not consistently demonstrate higher churn.

This highlights the importance of validating assumptions against observed data rather than assuming frequent service contact automatically indicates higher churn.

### 5. Early-tenure customers show elevated risk

Customers within their first **0–12 months** had the highest average risk score at approximately **4.06**, compared with approximately **1.84 among customers with 49+ months of tenure**.

### 6. Revenue exposure differs from risk alone

The **13–24 month tenure segment** represented the largest monthly revenue associated with churn at approximately **$384.8K**.

This demonstrates why retention prioritisation should consider both customer risk and financial exposure.

---

## Machine Learning

Five classification models were developed and compared:

1. Logistic Regression
2. Decision Tree
3. Random Forest
4. K-Nearest Neighbours
5. XGBoost

To prevent information leakage, variables derived directly from churn outcomes, retention activity and rule-based risk calculations were excluded from model training.

Numerical features were processed using median imputation and standardisation, while categorical variables were processed using most-frequent imputation and one-hot encoding.

The dataset was divided using a stratified 80/20 train-test split.

---

## Model Performance

| Model | Accuracy | Precision | Recall | F1 Score | ROC-AUC | PR-AUC |
|---|---:|---:|---:|---:|---:|---:|
| XGBoost | 62.8% | 40.6% | 63.2% | 49.5% | 0.677 | 0.457 |
| Random Forest | 61.8% | 39.0% | 57.7% | 46.6% | 0.652 | 0.420 |
| Decision Tree | 57.8% | 36.5% | 62.8% | 46.2% | 0.629 | 0.392 |
| Logistic Regression | 57.6% | 35.5% | 57.5% | 43.9% | 0.608 | 0.372 |
| KNN | 70.0% | 39.7% | 7.6% | 12.7% | 0.557 | 0.335 |

### Selected Model: XGBoost

**XGBoost** was selected as the final model because it provided the strongest overall performance for identifying customers likely to churn:

- **ROC-AUC:** 0.677
- **Churn Recall:** 63.2%
- **F1 Score:** 49.5%
- **PR-AUC:** 0.457

Although KNN achieved the highest overall accuracy at 70%, its churn recall was only 7.6%. This demonstrates why accuracy alone is not an appropriate model-selection metric for an imbalanced churn problem.

The final model therefore prioritises the ability to identify churners rather than simply maximising overall classification accuracy.

---

## Top Predictive Features

The stakeholder-facing XGBoost feature analysis identified several important predictive variables, including:

- Handset Price
- Credit Rating
- Occupation
- PRIZM Code
- Current Equipment Days
- Handset Refurbished
- Months in Service
- Marital Status
- Handset Web Capability
- Monthly Minutes

Feature importance represents **predictive association rather than causation**. These variables contributed to model predictions but should not automatically be interpreted as causal drivers of churn.

---

## Power BI Dashboard

The final Power BI solution contains five pages designed to move from executive-level monitoring to actionable retention strategy.

### Page 1 — Executive Overview

Provides a high-level view of customer churn, revenue exposure and retention priorities.

Key metrics include:

- Total Customers
- Churn Rate
- Monthly Revenue Associated with Churn
- Annualised Revenue
- High-Priority Customers
- Average Risk Score


### Page 2 — Churn Drivers

Investigates churn patterns across customer characteristics including:

- Revenue Band
- Customer Care Calls
- Device Age
- Frustration Level
- Overage Behaviour
- Predictive Drivers



### Page 3 — Customer Segmentation & Risk

Combines customer segmentation, churn risk and revenue exposure to identify retention priorities.

The page evaluates:

- Active high-priority customers
- Retention priority
- Churn rate by priority
- Revenue lost to churn
- Risk by tenure
- Revenue exposure by tenure



### Page 4 — Predictive Churn Analysis

Compares machine-learning models and communicates predictive performance through:

- Best Performing Model
- ROC-AUC
- Churn Recall
- F1 Score
- Model Performance Comparison
- ROC-AUC by Model
- Accuracy vs Churn Recall
- XGBoost Predictive Drivers


### Page 5 — Retention Strategy

Translates the analytical findings into business-focused retention recommendations.

Priority segments include:

- Early-tenure customers
- Established customers with high revenue exposure
- Active high-priority customers
- Medium-priority customers with elevated churn and revenue exposure

Recommended strategies include early intervention, onboarding support, loyalty incentives, personalised retention offers and targeted engagement.

---

## Business Recommendations

Based on the analysis, the following actions could be investigated and tested:

### Early-Tenure Intervention
Develop proactive onboarding and engagement strategies for customers within their first 12 months.

### Device Lifecycle Strategy
Investigate upgrade or device-related retention offers for customers using older equipment.

### Revenue-Based Prioritisation
Combine churn risk with customer revenue exposure rather than targeting customers based solely on predicted churn probability.

### Targeted Retention Campaigns
Prioritise active high-risk customers for personalised retention outreach and relevant offers.

### Monitor Overage Behaviour
Identify customers experiencing consistently high overage usage and test targeted plan or service interventions.

Retention actions should be validated through controlled experiments before assuming a causal impact on churn.

---

## Limitations

This project has several important limitations:

- The dataset is historical and does not represent a live production environment.
- Predictive relationships should not be interpreted as causal relationships.
- XGBoost achieved moderate predictive discrimination (ROC-AUC 0.677), leaving room for further model improvement.
- Customer behaviour may change over time, requiring model monitoring and retraining in a production environment.
- Proposed retention strategies would require experimentation to determine their actual impact.

---

## Future Improvements

Potential extensions include:

- Hyperparameter optimisation
- Cross-validation of the selected model
- Classification threshold optimisation
- SHAP-based model explainability
- Additional behavioural and temporal features
- Automated data pipelines
- Model monitoring and drift detection
- A/B testing of retention strategies
- Deployment of customer-level churn scoring

---

## Project Workflow

Data Collection  
↓  
Data Quality & Validation  
↓  
Data Cleaning  
↓  
Feature Engineering  
↓  
Exploratory Analysis  
↓  
SQL Analysis  
↓  
Customer Segmentation  
↓  
Power BI Dashboard  
↓  
Machine Learning  
↓  
Model Evaluation  
↓  
Retention Strategy

---



Skills demonstrated in this project:

`Python` `SQL` `Power BI` `DAX` `Data Analytics` `Machine Learning` `Data Validation` `Customer Analytics` `Business Intelligence` `Data Visualisation`
