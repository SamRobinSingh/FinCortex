# FinCortex: Financial Fraud Detection

## Project Description
This project presents an XGBoost model to proactively detect fraudulent financial transactions. Using a large simulation dataset, it identifies illicit 

TRANSFER and CASH_OUT activities where agents try to empty accounts. By using advanced feature engineering, this proactive solution enhances security and prevents financial loss.

---
  
## 1. Business Context 
The primary objective is to develop a robust model for predicting fraudulent transactions for a financial company. The insights derived from this model are used to create an actionable plan to enhance security infrastructure and proactively prevent fraudulent activities. The project is based on a simulated financial dataset mimicking real-world behavior over a 30-day period.

--- 

## 2. The Dataset 
The dataset is a synthetic log of financial transactions from a mobile money service.

- **Source:**  [Kaggle: Synthetic Financial Datasets for Fraud Detection](https://www.kaggle.com/datasets/ealaxi/paysim1/data)

- **Size:** 6.3 million transactions.

- **Timeframe:** A 30-day simulation where 1 step equals 1 hour.

- **Key Data Fields:**

- **type:** The type of transaction (CASH-IN, CASH-OUT, DEBIT, PAYMENT, TRANSFER).

- **amount:** The value of the transaction.

- **oldbalanceOrg / newbalanceOrig:** The balance of the originating customer before and after the transaction.

- **oldbalanceDest / newbalanceDest:** The balance of the recipient customer before and after the transaction.


- **isFraud:** A binary flag indicating if the transaction was determined to be fraudulent within the simulation.

- **isFlaggedFraud:** A system flag for attempts to transfer more than 200,000 in a single transaction.

---

## 3. Project Methodology 
The project followed a structured data science workflow to ensure robust and reliable results.

- **Exploratory Data Analysis (EDA):** A deep dive into the data revealed a severe class imbalance and confirmed that fraudulent activity was confined exclusively to TRANSFER and CASH_OUT transaction types. Statistical tests (t-tests) confirmed that transaction amount is a significant differentiator.

- **Feature Engineering:** New features were created to capture balance anomalies (errorBalanceOrig, errorBalanceDest). These features proved to be highly predictive, as they signal inconsistencies in financial ledger updates often associated with fraud.

- **Model Selection & Training:** An XGBoost (Extreme Gradient Boosting) classifier was chosen for its high performance on tabular data and its ability to handle class imbalance. The scale_pos_weight parameter was used to give more importance to fraudulent cases during training.

- **Evaluation:** The model was evaluated using metrics appropriate for imbalanced datasets, including Precision, Recall, AUC-ROC, and the Precision-Recall Curve. The model demonstrated excellent performance in distinguishing between fraudulent and legitimate transactions.

---

## 4. Key Findings & Insights 

- **Fraud Pattern Confirmed:** The model confirmed the primary fraud pattern: emptying an account via a high-value TRANSFER and a subsequent CASH_OUT.

- **Top Predictors:** The most important features for predicting fraud were balance errors, the initial balance of the originating account, the transaction amount, and whether the transaction was a transfer.

- **Actionable Intelligence:** The model provides a clear, data-driven profile of a fraudulent transaction, which can be used to build real-time prevention rules.

---

## 5. How to Use This Project 
To run this project on your local machine, follow these steps.

---

## Prerequisites
Python 3.9+

pip (Python package installer)

#### Installation & Execution

1. **Clone the repository:**
   ```bash
   git clone https://github.com/SamRobinSingh/FinCortex.git
   cd FinCortex
2. **Install dependencies:**
   It's recommended to use a virtual environment.
   
   ```bash
   pip install -r requirements.txt
3. **Download the Data**
   The dataset (Fraud.csv) is too large to be stored in this repository.
       
      - Download it from the Kaggle link provided above.
      - Place the Fraud.csv file in the root directory of this project.
4. **Run the script:**
   Execute the main Python script to run the analysis and train the model.
   ```bash
   python model.ipynb
   
---

# Project Report: Machine Learning for Financial Fraud Detection

## 1. Introduction and Objective
This report outlines the development of a machine learning model designed to detect fraudulent financial transactions. By analyzing a large transactional dataset, the project aims to identify patterns indicative of fraud and build an accurate predictive model. The ultimate goal is to provide a tool that can proactively flag suspicious activities, thereby enhancing security and mitigating financial losses.

---

## 2. Data Analysis and Preprocessing
The initial phase focused on understanding the dataset's structure and identifying key characteristics of fraudulent transactions.

Dataset Overview: The dataset consists of over 6.3 million transactions, with a very small fraction (approximately 0.13%) classified as fraudulent, indicating a severe class imbalance.

Probabilistic Insights: A crucial finding from the exploratory analysis is that fraudulent activities are exclusively confined to TRANSFER and CASH_OUT transaction types. The conditional probability of fraud for these types is significantly higher than for others, making them the primary focus of the model.

Statistical Validation: An independent t-test was conducted to compare the average transaction amounts between fraudulent and non-fraudulent activities. The results yielded a t-statistic of 48.61 and a p-value of 0.0, leading to the rejection of the null hypothesis. This confirms with statistical significance that the transaction amount is a critical differentiator between legitimate and fraudulent transactions.

Data Preparation:

Feature Engineering: Two new features, errorBalanceOrig and errorBalanceDest, were engineered to capture discrepancies in account balance updates, which can be strong indicators of manipulation.

Filtering: The dataset was filtered to include only TRANSFER and CASH_OUT types to focus the model on relevant data.

Encoding: The categorical type feature was converted into a numerical format using one-hot encoding.

---

## 3. Model Development and Training
An XGBoost (Extreme Gradient Boosting) classifier was selected for this task due to its high performance on imbalanced, tabular datasets.

Handling Class Imbalance: To address the severe class imbalance, the scale_pos_weight parameter was calculated and used. This technique assigns a higher penalty to misclassifying the minority class (fraud), compelling the model to pay closer attention to these critical but rare events.

Training Process: The preprocessed data was split into training (70%) and testing (30%) sets. The XGBoost model was then trained on the training data.

---

## 4. Model Performance and Evaluation
The model's performance was rigorously evaluated on the unseen test data.

Classification Report: The model demonstrated outstanding performance, achieving a precision of 96% and a recall of 80% for the fraudulent class. The overall F1-score for fraud detection was 87%, indicating a strong balance between precision and recall.

Confusion Matrix: The confusion matrix revealed that the model correctly identified 1,980 fraudulent transactions (True Positives) while missing 490 (False Negatives). It incorrectly flagged only 86 legitimate transactions as fraudulent (False Positives), showcasing a low false alarm rate.

Precision-Recall Curve: The Precision-Recall curve shows an Average Precision (AP) score of 0.899, further confirming the model's excellent capability to distinguish between classes even with the significant class imbalance.

---

## 5. Key Drivers of Fraud
The feature importance analysis from the XGBoost model identified the most influential factors in predicting fraudulent transactions.

**newbalanceOrig (35.5%):** The state of the originator's account balance after the transaction is the single most important predictor. A balance of zero often indicates an account being emptied.

**oldbalanceOrg (26.5%):** The initial balance of the originating account is also highly significant.

**newbalanceDest (14.9%):** The recipient's balance after the transaction.

**amount (8.9%):** The transaction amount itself.

**type_TRANSFER (6.8%):** Whether the transaction is a TRANSFER is a key indicator.

---

## 6. Conclusion
The developed XGBoost model is a highly effective tool for detecting financial fraud. It successfully identifies fraudulent transactions with high precision and recall by focusing on key transactional and behavioral patterns. The model's insights, particularly the importance of account balance changes and transaction types, provide a clear, data-driven foundation for building robust, real-time fraud prevention systems.


  
   
