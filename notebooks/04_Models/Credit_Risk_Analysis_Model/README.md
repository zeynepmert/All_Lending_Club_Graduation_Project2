Lending Club Credit Risk Analysis & Stress Testing Simulation

📌 Project Overview

This project aims to develop a robust Credit Risk Prediction Model using the Lending Club dataset. The primary objective is to predict the probability of default (PD) for individual loan applications and to simulate the portfolio's resilience under severe economic downturns through Stress Testing.

The workflow encompasses advanced data engineering, cost-sensitive machine learning modeling with Gradient Boosting, and macroeconomic scenario analysis.

Phase 1: Data Preparation and Integration

In this initial phase, a unified analytical dataset was constructed by integrating four distinct relational tables. This step was crucial to create a 360-degree view of the borrower and the loan characteristics.

1. Datasets Integrated

The final modeling dataset was formed by merging the following sources on the unique id key:

Loan Base: Core loan details (Amount, Interest Rate, Term, Grade).

Borrower Info: Demographic and financial data (Annual Income, Employment Length, Home Ownership).

Credit History: Historical credit utilization and limit information.

Delinquency Risk: Past delinquency events and public records.

2. Data Filtering & Target Definition

Target Variable: loan_status

Filtering: Only loans with a definitive outcome were retained:

Fully Paid $\rightarrow$ Encoded as 0 (Non-Default)

Charged Off $\rightarrow$ Encoded as 1 (Default)

Outcome: Current or late loans (not yet written off) were excluded to ensure binary classification clarity.

Phase 2: Data Cleaning, Preprocessing & Feature Engineering

The raw data contained structural inconsistencies and missing values that required statistical imputation and transformation strategies to prevent data leakage and ensure model stability.

1. Advanced Missing Value Handling

A strategy was devised to distinguish between "missing information" and "informative zeros":

Text-to-Numeric Conversion: Values like "Never" in columns tracking months since last delinquency were converted to 999 to represent a "clean history" numerically.

Statistical Imputation: * FICO Scores: Missing credit scores were imputed using the training set mean.

Financial Ratios: Other numerical gaps were filled with 0 where appropriate, ensuring no future data leakage into the training process.

2. Categorical Encoding

One-Hot Encoding: Applied to categorical variables such as home_ownership (e.g., RENT, OWN, MORTGAGE) to convert them into a machine-readable binary format, avoiding ordinal misconceptions.

3. Train/Test Split

Split Ratio: 80% Training / 20% Testing.

Stratification: Utilized stratify=y to ensure the proportion of default loans remained consistent across both training and testing sets.

Phase 3: Cost-Sensitive Model Training

Standard machine learning models often bias towards the majority class (Safe Loans). To address the inherent Class Imbalance in credit data, a Cost-Sensitive Learning approach was adopted.

1. Model Selection & Configuration

Algorithm: Gradient Boosting Classifier

Hyperparameters:

n_estimators=300 (Increased for better learning capacity)

learning_rate=0.1

max_depth=5 (To capture non-linear complex patterns)

subsample=0.9 (To prevent overfitting)

2. Addressing Imbalance: Smart Weighting

Instead of synthetic oversampling (SMOTE), a Sample Weighting strategy was implemented:

Weighting Logic: A manual weight of 2.5 was assigned to the minority class (Charged Off).

Rationale: This penalizes the model 2.5x more for missing a default than for a false alarm, aligning the model with the bank's risk aversion strategy.

3. Performance Metrics

The optimized model achieved a "Sweet Spot" between risk detection and business opportunity:

Metric

Value

Interpretation

Accuracy

74.35%

High reliability in overall predictions.

ROC-AUC

0.72

Good capability to distinguish between defaulters and payers.

Recall (Class 1)

0.46

Captures nearly half of all potential defaults (up from 4% in the baseline model).

Phase 4: Stress Testing & Macroeconomic Analysis

Beyond static prediction, the project evaluated how the portfolio would perform under hypothetical economic crises.

1. "Deep Recession" Scenario Simulation

A hard stress test was applied to the test set by manipulating key macroeconomic variables:

📉 Income Shock: Borrower annual incomes reduced by 40%.

📈 Debt Burden: Debt-to-Income (DTI) ratios increased by 50%.

🔻 Credit Score Decay: FICO scores lowered by 50 points.

💸 Interest Rate Spike: Lending rates increased by 30%.

2. Stress Test Results

Baseline Risk (Normal Economy): 23.90% predicted default rate.

Crisis Risk (Deep Recession): 45.80% predicted default rate.

Insight: The +21.90% surge in risk demonstrates the model's sensitivity to macroeconomic shifts and highlights the need for increased capital buffers during economic downturns.

3. Historical Validation (Vintage Analysis)

A dual-axis analysis compared Lending Club's historical default rates against US Unemployment Rates (2007-2018).

Findings: A strong correlation was observed during the 2008 Financial Crisis, validating the model's assumption that macro-factors drive credit risk. An anomaly in 2015-2016 (high defaults despite low unemployment) revealed internal risk policy shifts within the platform.

Final Assessment

This project successfully delivered a Risk-Averse Credit Model that:

Protects Capital: By prioritizing the detection of defaulters (Higher weights).

Ensures Business Continuity: By maintaining a healthy accuracy rate (74%), avoiding excessive rejection of good customers.

Future-Proofs the Portfolio: By quantifying potential losses under severe economic stress scenarios.