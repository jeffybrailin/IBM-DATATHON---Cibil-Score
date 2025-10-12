# Bharat Score – AI-Powered Financial Inclusion 

**Team:** The 900 Club 

**Members:** Rhudhresh R, Raanesh U, Ranjith Ganesh B, Jeffy Brailin T  

---

## Problem Statement :
Traditional credit scoring models exclude millions who lack a formal credit history, especially in emerging markets.  
This exclusion restricts access to financial services and prevents economically capable individuals from obtaining credit.

---

## Proposed Solution :
**Bharat Score** is an **AI-powered financial inclusion system** that leverages **alternative data sources** such as monthly expenses, Credit card bills, EMI behavior, and stability indicators alongside traditional credit data to create a **reliable and transparent credit score**.

It aims to empower financial institutions to assess credit risk more accurately and extend fair credit access to all.

---

## Three-Channel Architecture :

1. **Channel 1: Bureau Intelligence**  
   - Uses traditional CIBIL and credit bureau data.  
   - Covers ~60% of the credit-active population.  
   - Provides baseline creditworthiness assessment.  

2. **Channel 2: Cashflow Analytics**  
   - Analyzes UPI transaction patterns, EMI ratios, and payment regularity.  
   - Captures real-time digital payment behavior from India’s $200B+ payment ecosystem.  

3. **Channel 3: Stability Signals**  
   - Uses address stability, demographic data, and other alternative indicators.  
   - Targets “thin-file” users with limited or no formal credit history.  

---

## Bharat Score Formula :

**Exact Formula :**  Bharat Score = 300 + [ log(Combinedodds) / log(2) ] * PDO


### Term Definitions :
- **Bharat Score:** Final score ranging from **300 to 900**, where higher values indicate lower risk.
  
- **Combinedodds:** Aggregate ratio of positive to negative outcomes derived from multiple data signals.
  
- **log(2):** Constant used to normalize scale.
  
- **PDO (Points to Double the Odds):** Scaling constant defining how many points are needed to double the odds of a positive outcome.

---

## Dataset Overview – Home Credit Default Risk

| File Name | Description |
|------------|-------------|
| **application_train/test.csv** | Main table; one row per loan. `Train` includes `TARGET`, `Test` does not. Contains static loan & applicant info. |
| **bureau.csv** | Historical credits reported to Credit Bureau for each applicant; multiple rows per previous loan. |
| **bureau_balance.csv** | Monthly balances for previous credits in the bureau; one row per month per previous loan. |
| **POS_CASH_balance.csv** | Monthly snapshots of previous POS and cash loans with Home Credit; one row per month per previous loan. |
| **credit_card_balance.csv** | Monthly snapshots of past credit card accounts; one row per month per previous card. |
| **previous_application.csv** | Records of all previous Home Credit applications; one row per application. |
| **installments_payments.csv** | Repayment history for previous Home Credit loans; one row per payment or missed installment. |
| **HomeCredit_columns_description.csv** | Descriptions of all columns in the above datasets. |

---

## Workflow :

1. **Data Ingestion :** Loaded and cleaned all datasets.

2. **Exploratory Data Analysis :** Understood data distributions, missing values, correlations, and feature importance across all datasets.  
  
3. **Feature Engineering:** Aggregated and encoded features from all channels (bureau, POS, cashflow, etc.).
   
4. **Model Training:** Trained LightGBM model and Ensemble models to predict default risk (`TARGET`).
   
5. **Score Calibration:** Converted the model output (odds) to standardized Bharat Score using the given formula.
   
6. **Evaluation:** Validated using AUC, KS-score, and distribution fairness metrics.

---

## Datasets

We used the following datasets for our project.  

> **Note:** The datasets are large. We chose larger datasets to ensure the model performs extraordinarily well and captures all possible patterns. Hence, we are providing links instead of uploading the files directly.  

1. **Home Credit Default Risk**  
   [https://www.kaggle.com/competitions/home-credit-default-risk/data](https://www.kaggle.com/competitions/home-credit-default-risk/data)  

2. **Credit Score Classification**  
   [https://www.kaggle.com/datasets/parisrohan/credit-score-classification](https://www.kaggle.com/datasets/parisrohan/credit-score-classification)







