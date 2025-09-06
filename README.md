# FinCortex: Financial Fraud Detection

## Project Description
This project presents an XGBoost model to proactively detect fraudulent financial transactions. Using a large simulation dataset, it identifies illicit 

TRANSFER and CASH_OUT activities where agents try to empty accounts. By using advanced feature engineering, this proactive solution enhances security and prevents financial loss.

---

## 1. Business Context 📈
The primary objective is to develop a robust model for predicting fraudulent transactions for a financial company. The insights derived from this model are used to create an actionable plan to enhance security infrastructure and proactively prevent fraudulent activities. The project is based on a simulated financial dataset mimicking real-world behavior over a 30-day period.

---

## 2. The Dataset 📊
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

## 5. How to Use This Project 🛠
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



  
   
