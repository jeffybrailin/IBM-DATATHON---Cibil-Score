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

# Loan Default Prediction Dataset

## Introduction
The purpose of using this dataset is to use historical loan application data to predict whether an applicant will be able to repay a loan. This is a **supervised classification task**.

- **Supervised**: Labels (outcomes) are included in the training data. The model learns to predict labels from features.
- **Classification**: The label is binary:
  - `0` → Will repay the loan on time
  - `1` → Will have difficulty repaying the loan

---

## Dataset Fields

| Field | Description |
|-------|-------------|
| SK_ID_CURR | Current application ID |
| TARGET | Loan repayment risk: 1 - high risk; 0 - low risk |
| NAME_CONTRACT_TYPE | Type of loan: cash or revolving (renewable credit, one-time application with multiple withdrawals) |
| CODE_GENDER | Applicant’s gender |
| FLAG_OWN_CAR | Does the applicant own a car? |
| FLAG_OWN_REALTY | Does the applicant own real estate? |
| CNT_CHILDREN | Number of children of the applicant |
| AMT_INCOME_TOTAL | Applicant’s total income |
| AMT_CREDIT | Amount of loan requested |
| AMT_ANNUITY | Loan annuity |
| AMT_GOODS_PRICE | If consumer loan, the actual price of the product |
| NAME_TYPE_SUITE | People accompanying the applicant during the application |
| NAME_INCOME_TYPE | Applicant’s type of income |
| NAME_EDUCATION_TYPE | Applicant’s education level |
| NAME_FAMILY_STATUS | Applicant’s marital status |
| NAME_HOUSING_TYPE | Applicant’s housing situation (rent, own, live with parents, etc.) |
| REGION_POPULATION_RELATIVE | Population density of applicant’s region (normalized) |
| DAYS_BIRTH | Birth date (in days before application, negative value) |
| DAYS_EMPLOYED | Length of employment in current job (in days before application, negative value) |
| DAYS_REGISTRATION | Last time applicant updated registration info (days before application, negative) |
| DAYS_ID_PUBLISH | Last time applicant updated ID for this application (days before application, negative) |
| FLAG_MOBIL | Applicant provided a mobile number (1-yes, 0-no) |
| FLAG_EMP_PHONE | Applicant provided a landline phone (1-yes, 0-no) |
| FLAG_WORK_PHONE | Applicant provided a work phone (1-yes, 0-no) |
| FLAG_CONT_MOBILE | Mobile number can be contacted (1-yes, 0-no) |
| FLAG_EMAIL | Applicant provided an email (1-yes, 0-no) |
| OCCUPATION_TYPE | Applicant’s occupation |
| REGION_RATING_CLIENT | Company rating of applicant’s region (1, 2, 3) |
| REGION_RATING_CLIENT_W_CITY | Company rating of applicant’s region considering city (1, 2, 3) |
| WEEKDAY_APPR_PROCESS_START | Weekday when application started |
| HOUR_APPR_PROCESS_START | Hour when application started |
| REG_REGION_NOT_LIVE_REGION | Match between permanent and contact address (1-no, 2-yes, regional level) |
| REG_REGION_NOT_WORK_REGION | Match between permanent and work address (1-no, 2-yes, regional level) |
| LIVE_REGION_NOT_WORK_REGION | Match between contact and work address (1-no, 2-yes, regional level) |
| REG_CITY_NOT_LIVE_CITY | Match between permanent and contact address (1-no, 2-yes, city level) |
| REG_CITY_NOT_WORK_CITY | Match between permanent and work address (1-no, 2-yes, city level) |
| LIVE_CITY_NOT_WORK_CITY | Match between contact and work address (1-no, 2-yes, city level) |
| ORGANIZATION_TYPE | Type of organization where applicant works |
| EXT_SOURCE_1 / 2 / 3 | Standardized scores from external data sources |
| APARTMENTS_AVG → EMERGENCYSTATE_MODE | Standardized scores of applicant’s living environment indicators |
| OBS_30_CNT_SOCIAL_CIRCLE → DEF_60_CNT_SOCIAL_CIRCLE | Related to social circle and defaults (exact meaning unclear) |
| DAYS_LAST_PHONE_CHANGE | Last time applicant changed phone number (days before application, negative) |
| FLAG_DOCUMENT_2 → FLAG_DOCUMENT_21 | Whether applicant provided additional documents 2, 3, 4, ..., 21 |
| AMT_REQ_CREDIT_BUREAU_HOUR | Number of credit bureau inquiries in the last hour |
| AMT_REQ_CREDIT_BUREAU_DAY | Number of credit bureau inquiries in the last day |
| AMT_REQ_CREDIT_BUREAU_WEEK | Number of credit bureau inquiries in the last week |
| AMT_REQ_CREDIT_BUREAU_MONTH | Number of credit bureau inquiries in the last month |
| AMT_REQ_CREDIT_BUREAU_QRT | Number of credit bureau inquiries in the last quarter |
| AMT_REQ_CREDIT_BUREAU_YEAR | Number of credit bureau inquiries in the last year |

---

## Notes
- `OBS_30_CNT_SOCIAL_CIRCLE → DEF_60_CNT_SOCIAL_CIRCLE`: Likely related to the number of social contacts who have defaulted or observed financial behavior. Exact meaning is unclear.  
- `APARTMENTS_AVG → EMERGENCYSTATE_MODE`: Aggregated metrics about applicant’s living conditions (apartment quality, utilities, etc.).

---

## Usage
This dataset can be used to train supervised machine learning models to predict loan repayment risks.

- **Task Type**: Binary Classification
- **Target Variable**: `TARGET`



