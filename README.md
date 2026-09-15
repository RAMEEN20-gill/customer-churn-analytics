# Customer Churn Prediction & Business Intelligence

## Project Overview

Customer churn is a major business challenge for subscription-based companies. Losing customers can directly impact revenue, making it important for businesses to identify customers who are likely to churn and take proactive retention actions.

This project develops an end-to-end **Customer Churn Prediction and Business Intelligence solution** using machine learning and Power BI.

The project combines:

* Data cleaning and preprocessing
* Exploratory data analysis
* Feature engineering
* Machine learning classification
* Churn probability prediction
* Customer risk segmentation
* Business-oriented retention recommendations
* Interactive Power BI dashboards

The final solution moves from:

**Raw Customer Data → Data Preparation → ML Prediction → Risk Segmentation → Business Insights → Retention Actions**

##  Project Objectives

The main objectives of this project are to:

1. Analyze customer behavior and churn patterns.
2. Prepare and clean the Telco Customer Churn dataset.
3. Engineer additional features to improve the analysis.
4. Train machine learning models to predict customer churn.
5. Compare XGBoost and Random Forest models.
6. Generate churn probabilities for individual customers.
7. Segment customers into Low, Medium, and High Risk.
8. Estimate monthly revenue at risk.
9. Recommend retention actions based on customer risk and characteristics.
10. Build interactive Power BI dashboards for business decision-making.


##  Dataset

The project uses the **Telco Customer Churn dataset** containing **7,043 customer records**.

The dataset contains customer demographic information, account information, subscribed services, billing information, and churn status.

### Main Features

| Category             | Features                                                    |
| -------------------- | ----------------------------------------------------------- |
| Customer Information | CustomerID, Gender, SeniorCitizen, Partner, Dependents      |
| Account Information  | Tenure, Contract, PaperlessBilling                          |
| Services             | PhoneService, MultipleLines, InternetService                |
| Additional Services  | OnlineSecurity, OnlineBackup, DeviceProtection, TechSupport |
| Streaming            | StreamingTV, StreamingMovies                                |
| Billing              | MonthlyCharges, TotalCharges, PaymentMethod                 |
| Target               | Churn                                                       |



##  Data Preparation

The dataset was cleaned and prepared before model development.

### Data preprocessing included:

* Inspecting dataset structure and data types
* Handling missing values
* Converting `TotalCharges` from text to numeric
* Encoding categorical variables
* Preparing numerical features
* Creating derived business features
* Splitting the data into training and testing sets

The final modeling dataset contains:

**7,043 rows and 23 features**

The data was divided into:

* **Training set:** 5,634 customers
* **Testing set:** 1,409 customers


##  Feature Engineering

Three additional features were created to improve the business analysis and modeling:

### 1. AverageMonthlySpend

Provides an additional measure of customer spending based on account charges and tenure.

### 2. ServiceCount

Represents the number of subscribed services for each customer.

### 3. HasTechSupport

A simplified indicator representing whether the customer has technical support.

These features provide additional information about customer engagement, spending, and service usage.


## Machine Learning Models

Two classification models were developed and evaluated:

### XGBoost

XGBoost was selected as the primary model because it provided the strongest ROC-AUC performance.

Key parameters included:

* `n_estimators = 200`
* `max_depth = 4`
* `learning_rate = 0.05`
* `colsample_bytree = 0.8`
* `eval_metric = logloss`

### Random Forest

Random Forest was also trained as a comparison model.


##  Model Performance

### XGBoost

| Metric    |      Score |
| --------- | ---------: |
| Accuracy  |     80.20% |
| Precision |     65.99% |
| Recall    |     52.41% |
| F1 Score  |     58.42% |
| ROC-AUC   | **84.42%** |

### Random Forest

| Metric  |  Score |
| ------- | -----: |
| ROC-AUC | 82.70% |

Based on ROC-AUC, **XGBoost performed better than Random Forest** and was selected as the primary model.


##  Important Predictors

The most influential features in the XGBoost model included:

| Feature                           | Importance |
| --------------------------------- | ---------: |
| Contract — Two year               |     19.73% |
| Internet Service — Fiber optic    |     18.39% |
| Contract — One year               |     12.28% |
| Internet Service — No             |      7.33% |
| Payment Method — Electronic check |      6.57% |
| Tenure                            |      4.13% |

These results indicate that **contract type, internet service, payment method, and customer tenure** are important factors associated with predicted churn.



##  Churn Threshold Optimization

The default classification threshold of 0.50 was evaluated along with alternative thresholds.

Because customer retention is an important business objective, a threshold of **0.35** was selected for the operational prediction analysis.

At a threshold of 0.35:

| Metric    |      Value |
| --------- | ---------: |
| Precision |     55.69% |
| Recall    |     71.93% |
| F1 Score  | **62.78%** |

The lower threshold increases recall, allowing the business to identify more potentially at-risk customers for retention campaigns.


##  Customer Risk Segmentation

Customers were divided into three risk categories based on predicted churn probability:

| Risk Level  | Probability  |
| ----------- | ------------ |
| Low Risk    | < 35%        |
| Medium Risk | 35% – 69.99% |
| High Risk   | ≥ 70%        |

### Risk Distribution

* **Low Risk:** 67.26%
* **Medium Risk:** 23.77%
* **High Risk:** 8.97%

Approximately **632 customers** were classified as High Risk.


##  Revenue at Risk

The project also translates churn predictions into a business-oriented financial metric.

Customers predicted to churn represent approximately:

### **$174,705.70 in monthly revenue at risk**

Within the High Risk segment:

### **$51,870.50 in monthly revenue at risk**

This allows the model's output to be interpreted not only as a machine learning prediction but also as a potential business impact.


##  Retention Recommendations

The project includes rule-based recommendations based on customer risk and characteristics.

Examples include:

* **High Risk + Month-to-month contract**

  * Offer annual contract discount + proactive support

* **High Risk + high MonthlyCharges**

  * Offer personalized discount + premium support

* **High Risk**

  * Priority retention outreach + support follow-up

* **Medium Risk + Month-to-month contract**

  * Offer contract upgrade incentive

* **Lower Risk customers**

  * Continue regular engagement

This creates a business workflow:

**Prediction → Risk → Customer Prioritization → Recommended Action**


# Power BI Dashboards

The project includes three Power BI report pages designed for different levels of business analysis.

## Dashboard 1 — Executive Churn Overview

This dashboard provides a high-level view of customer churn and business impact.

### Key components

* Total Customers
* Predicted Churn
* Predicted Churn Rate
* High Risk Customers
* Monthly Revenue at Risk
* Customer Risk Distribution
* Revenue at Risk by Risk Level
* Predicted Churn by Contract
* Predicted Churn by Internet Service
* Predicted Churn by Payment Method

### Dashboard Preview

![Executive Churn Overview](powerbi/Dashboard_1.png)


## Dashboard 2 — Customer Risk & Retention

This dashboard focuses on customer risk segmentation and retention-related patterns.

### Key components

* High Risk Customers
* High Risk Revenue
* Medium Risk Customers
* Predicted Churn
* Risk-level distribution
* Contract analysis
* Internet Service analysis
* Payment Method analysis

### Dashboard Preview

![Customer Risk & Retention](powerbi/Dashboard_2.png)


## Dashboard 3 — Customer Retention Action Center

The third dashboard is designed as an operational decision-support page.

Its purpose is to answer:

> **Which customers should the business prioritize, and what action should be taken?**

### Key components

* High Risk Customers
* High Risk Revenue
* Customers Requiring Attention
* Contract slicer
* Internet Service slicer
* Payment Method slicer
* Top High-Risk Customers table
* Churn Probability
* Risk Level
* Recommended Retention Action

### Dashboard Preview

![Customer Retention Action Center](powerbi/Dashboard_3.png)

---

# 🗂️ Project Structure

```text
customer-churn-project/
│
├── data/
│   ├── raw/
│   │
│   └── processed/
│       ├── Telco-Customer-Churn-cleaned.csv
│       ├── customer_churn_predictions.csv
│       └── churn_dashboard_data.csv
│
├── models/
│   ├── xgb_model.pkl
│   └── preprocessor.pkl
│
├── notebooks/
│   ├── 01_data_inspection.ipynb
│   ├── 02_final_prediction.ipynb
│   └── 03_business_intelligence.ipynb
│
├── dashboard/
│   ├── Customer_Churn_Analytics.pbix
│   ├── Dashboard_1.png
│   ├── Dashboard_2.png
│   └── Dashboard_3.png
│
├── README.md


#  Technologies Used

### Programming & Data Analysis

* Python
* Pandas
* NumPy
* Scikit-learn
* XGBoost
* Matplotlib

### Machine Learning

* XGBoost
* Random Forest
* Classification
* Probability-based prediction
* Threshold optimization
* Feature importance analysis

### Business Intelligence

* Microsoft Power BI
* DAX
* Interactive slicers
* KPI cards
* Tables
* Conditional formatting
* Business-focused dashboards

### Development Environment

* Jupyter Notebook
* Visual Studio Code
* Git
* GitHub


#  Notebooks

### `01_data_inspection.ipynb`

Contains:

* Dataset inspection
* Data types
* Missing-value analysis
* Exploratory analysis
* Churn distribution
* Business-level observations

### `02_final_prediction.ipynb`

Contains:

* Feature engineering
* Data preprocessing
* Model training
* XGBoost
* Random Forest
* Model evaluation
* Feature importance
* Threshold tuning
* Churn prediction
* Customer risk classification
* Retention recommendations
* Model saving

### `03_business_intelligence.ipynb`

Contains:

* Loading prediction results
* Preparing dashboard data
* Revenue-at-risk calculations
* Creating the Power BI dataset
* Exporting processed data for visualization


#  Key Business Insights

The analysis identified several important patterns:

* Customers on **month-to-month contracts** have substantially higher churn than customers on longer-term contracts.
* **Fiber optic customers** show a higher observed churn rate than DSL customers.
* Customers using **electronic check** as their payment method show relatively high churn.
* Customers with **technical support** have lower observed churn than customers without technical support.
* Longer-tenure customers generally show lower churn risk.
* High-risk customers represent a smaller portion of the total customer base but account for a significant amount of potential monthly revenue at risk.

These insights can help businesses prioritize retention campaigns instead of treating all customers equally.

---

# 🔄 End-to-End Workflow

```text
Raw Telco Customer Data
          ↓
Data Inspection & Cleaning
          ↓
Exploratory Data Analysis
          ↓
Feature Engineering
          ↓
Data Preprocessing
          ↓
Train/Test Split
          ↓
XGBoost + Random Forest
          ↓
Model Evaluation
          ↓
Threshold Optimization
          ↓
Churn Probability
          ↓
Risk Segmentation
          ↓
Revenue-at-Risk Analysis
          ↓
Retention Recommendations
          ↓
Power BI Dashboards
          ↓
Business Decision Support
```

---

# 🚀 How to Run the Project

## 1. Clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/customer-churn-analytics.git
cd customer-churn-analytics
```

Replace `YOUR-USERNAME` with your GitHub username.

## 2. Create a virtual environment

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

## 3. Install dependencies

```bash
pip install -r requirements.txt
```

## 4. Run the notebooks

Open the notebooks in Jupyter Notebook or VS Code and run them in the following order:

```text
01_data_inspection.ipynb
        ↓
02_final_prediction.ipynb
        ↓
03_business_intelligence.ipynb
```

## 5. Open the Power BI report

Open:

```text
powerbi/Customer_Churn_Analytics.pbix
```

using **Microsoft Power BI Desktop**.

---

# 📁 Output Files

The project generates several important outputs:

### `customer_churn_predictions.csv`

Contains customer-level:

* Churn probability
* Predicted churn
* Risk level
* Customer characteristics
* Recommended retention action

### `churn_dashboard_data.csv`

Contains the processed data used to build the Power BI dashboards, including:

* Customer information
* Churn probability percentage
* Risk level
* Monthly revenue at risk
* Recommended action

### Model files

```text
models/xgb_model.pkl
models/preprocessor.pkl
```

These allow the trained model and preprocessing pipeline to be reused.

---

# 💡 Future Improvements

Possible future improvements include:

* Hyperparameter optimization using cross-validation
* Model explainability using SHAP
* Automated customer retention campaigns
* Real-time churn prediction
* Integration with a CRM system
* Customer lifetime value analysis
* Automated Power BI data refresh
* Deployment of the prediction model as an API
* Monitoring model performance over time


# ⚠️ Disclaimer

This project is intended for educational, portfolio, and analytical purposes.

The churn predictions represent model-based probabilities and should be used as decision-support information rather than as definitive predictions of individual customer behavior.

## 👩‍💻 Author

Rameen

Computer Science Student
Focus: Data Analytics, Business Intelligence & Data-Driven Decision Making


## ⭐ Project Summary

This project demonstrates an end-to-end approach to solving a business problem using **data analytics, machine learning, and business intelligence**.

Rather than stopping at predicting churn, the project connects machine learning results with **customer risk segmentation, financial impact analysis, and actionable retention recommendations**, providing a complete analytics workflow from data to business decision-making.
