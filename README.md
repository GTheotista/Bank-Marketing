# Bank Marketing Prediction

## **Project Overview**
In the competitive banking industry, financial institutions strive to attract and retain customers efficiently. One of the key banking products is term deposits, which provide customers with a secure investment option while ensuring stable funding for the bank. However, not all customers are equally likely to invest in term deposits, making it crucial for banks to identify potential customers and target them with effective marketing campaigns.

This project aims to predict whether a customer will subscribe to a term deposit based on historical bank marketing data. By analyzing customer demographics and past interactions, we build a machine learning model to improve marketing efficiency and maximize customer acquisition.

## **Dataset**
The dataset used in this project is the **[Bank Marketing Dataset](https://drive.google.com/drive/folders/13lrEDlKfnTPNREfGLBaYGYf8dSjHBzfW)** from the Purwadhika's School. It contains details of bank clients, their previous interactions, and the outcome of marketing campaigns.

### **Feature Groups**
The dataset consists of two main feature groups:

1. **Customer Profile**
   - **Age:** The age of the customer.
   - **Job:** The customer's occupation.
   - **Balance:** The customer's account balance.
   - **Housing:** Whether the customer has a housing loan (yes/no).
   - **Loan:** Whether the customer has a personal loan (yes/no).

2. **Marketing Data**
   - **Contact:** The type of communication used to contact the customer.
   - **Month:** The last month of the year in which the customer was contacted.
   - **Campaign:** The number of contacts made during the current campaign for this customer.
   - **Pdays:** The number of days since the customer was last contacted in the previous campaign.
   - **Poutcome:** The outcome of the previous marketing campaign (e.g., success or failure).
   - **Deposit:** Whether the customer made a term deposit or not (target variable).

## **Data Understanding & Cleaning**
- **Handling Outliers**: Outliers were detected and handled appropriately.
- **Feature Analysis**: Distribution of categorical features was analyzed in relation to the target variable.
- **Correlation Analysis**: Relationships between numerical features were examined.

## **Data Preparation**
A data preprocessing pipeline was developed to clean, transform, and encode the dataset before training a machine learning model. It consists of:

### **Preprocessing Steps**
- **Month Conversion & Cyclic Encoding:** Converts categorical months into numerical values (1–12) and applies sin/cos encoding to preserve cyclic relationships.
- **Job Category Grouping:** Jobs with fewer than 250 occurrences were grouped as "Other" and further categorized into broader groups.
- **Handling Pdays:** Created a new binary feature `not_contacted` (1 if the client was never contacted). Replaced `pdays = -1` with the maximum `pdays` value.
- **Binary Encoding:** Converted `housing` and `loan` features from "yes"/"no" to 1/0.

### **Column Transformer Pipeline**
- **Numerical Features (age, balance, campaign, pdays, month_sin, month_cos)**
  - Missing values were imputed with the median.
  - StandardScaler was applied for normalization.
- **Categorical Features (job, contact, poutcome)**
  - Missing values were imputed with the most frequent value.
  - One-Hot Encoding was applied, ignoring unknown categories.
- **Binary Features (housing, loan, not_contacted)**
  - Passed through without transformation.

## **Model Training & Evaluation**
Six machine learning models were trained and evaluated:
- **Logistic Regression**
- **K-Nearest Neighbors (KNN)**
- **Decision Tree Classifier**
- **Random Forest Classifier**
- **XGBoost Classifier**
- **LightGBM Classifier**

After evaluating performance on cross-validation and test data, **LightGBM was selected as the best model**.

### **Handling Class Imbalance**
- **Random Over-Sampling (ROS):** Applied to balance the dataset.
- **Evaluation Results:** ROS improved recall and overall model performance, making it the preferred approach.

### **Hyperparameter Tuning**
- **Grid Search:** Performed to optimize model parameters.
- **Results:** Tuned LightGBM showed improved performance over the default model.

## **Feature Importance Analysis**
- The top 10 most important features were extracted from the best LightGBM model.
- A bar plot was generated to visualize the most influential factors affecting customer subscription decisions.

## **Results & Conclusion**
- **Final Model Performance:**
  - **Accuracy:** 69%
  - **Precision for Class 1 (Subscribers):** 67%
  - **Recall for Class 1 (Subscribers):** 66%
  - **F1-Score:** 0.67
- **Key Insights:**
  - The model effectively identifies potential subscribers, with **recall prioritized** to maximize customer acquisition.
  - The tuning process improved the balance between recall and precision.
  - Banks can leverage these insights to refine targeted marketing campaigns and improve efficiency.

---
**Author:** Giovanny Theotista

