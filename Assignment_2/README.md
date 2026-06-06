# Assignment 2: End-to-End Machine Learning Pipeline

## Business Account Upgrade Prediction Using Logistic Regression

## Course Information

**Course:** MBAI 5310G – AI Programming
**Assignment:** Assignment 2 – End-to-End Machine Learning Pipeline
**Model Used:** Logistic Regression Baseline Model
**Dataset:** `business_account_upgrade_prediction_dataset.csv`

---

## Project Overview

This project develops a basic end-to-end machine learning pipeline to predict whether a business account will upgrade its account or not.

The purpose of this assignment is to demonstrate the full machine learning workflow, starting from understanding the business problem and preparing the dataset, to training a baseline classification model and interpreting the results from a business perspective.

The model uses business account information, account activity, revenue details, product usage, support history, sales contact status, and training-related information to predict the target variable: `Upgraded_Account`.

---

## Business Problem

Many businesses offer different account plans or service levels to their customers. Some business accounts may remain on their current plan, while others may upgrade to a higher-value account.

The main business problem is to identify which business accounts are more likely to upgrade. This prediction can help the company improve sales planning, customer relationship management, training support, and targeted marketing strategies.

The key business question is:

**Can the company predict whether a business account will upgrade using account information, revenue details, transaction activity, product usage, support history, sales contact information, and customer engagement indicators?**

A machine learning model can help the business prioritize accounts for sales follow-up, customer success support, product demonstrations, training programs, account reviews, or targeted upgrade offers.

---

## Dataset Description

The dataset used in this project is:

```text
business_account_upgrade_prediction_dataset.csv
```

Each row represents one business account. The dataset contains account-level information such as:

* Company size
* Industry
* Annual revenue
* Monthly transactions
* Current plan
* Account age in months
* Support tickets
* Sales contact status
* Product usage score
* Monthly fee
* Training attendance
* Upgrade status

The target variable is:

```text
Upgraded_Account
```

This variable has two possible values:

* `Yes` – the business account upgraded
* `No` – the business account did not upgrade

Since the target variable has two possible categories, this is a supervised binary classification problem.

---

## Features and Target Variable

### Target Variable

```text
Upgraded_Account
```

This is the variable the model is trying to predict.

### Input Features

The selected feature variables are:

```text
Company_Size
Industry
Annual_Revenue
Monthly_Transactions
Current_Plan
Account_Age_Months
Support_Tickets
Sales_Contacted
Product_Usage_Score
Monthly_Fee
Training_Attended
```

The column `Account_ID` was removed before model training because it is only an identifier and does not provide meaningful predictive information.

---

## Machine Learning Pipeline

The notebook follows a complete end-to-end machine learning pipeline:

1. Import required libraries
2. Load the dataset
3. Inspect the dataset
4. Understand the business problem
5. Identify the target variable and input features
6. Check numerical and categorical variables
7. Clean the dataset
8. Handle missing values
9. Define `X` and `y`
10. Split the data into training and testing sets
11. Apply preprocessing
12. Train a Logistic Regression baseline model
13. Make predictions on the testing data
14. Evaluate the model
15. Interpret the results from a business perspective
16. Discuss model limitations
17. Reflect on responsible AI use
18. Provide a final conclusion

---

## Preprocessing Approach

The dataset contains both numerical and categorical variables. Different preprocessing steps were applied to each type of feature.

### Numerical Features

Numerical features were scaled using:

```text
StandardScaler
```

Scaling is important for Logistic Regression because numerical features may have different value ranges.

### Categorical Features

Categorical features were converted into numerical format using:

```text
OneHotEncoder
```

This is required because machine learning models cannot directly process text-based categories.

### ColumnTransformer

A `ColumnTransformer` was used to apply the correct preprocessing method to each feature type. This keeps the workflow organized and consistent.

---

## Model Used

The baseline model used in this assignment is:

```text
Logistic Regression
```

Logistic Regression was selected because it is simple, interpretable, and commonly used for binary classification problems.

The purpose of using a baseline model is to establish an initial performance level. More advanced models can be compared against this baseline in future work.

---

## Model Evaluation Results

The Logistic Regression model was evaluated using the testing dataset.

### Main Result

The model achieved an accuracy of approximately:

```text
75.68%
```

This means the model correctly predicted about 76% of the test records.

### Evaluation Metrics

The model was evaluated using:

* Accuracy
* Precision
* Recall
* F1-score
* Confusion matrix
* Classification report

### Business Interpretation

The model performs better at predicting accounts that did not upgrade than accounts that upgraded. This may be partly because the dataset contains more `No` values than `Yes` values.

From a business perspective, the model can help identify business accounts that may be suitable for sales follow-up, customer success support, training, engagement, or upgrade-related actions.

However, the model should be used as a decision-support tool rather than a final decision-making system.

---

## Limitations

One limitation of this model is class imbalance. The dataset contains more accounts that did not upgrade than accounts that upgraded. As a result, the model may perform better for the majority class and may be weaker at identifying upgraded accounts.

Another limitation is that the model is based only on the variables available in the dataset. Real business account upgrade decisions may depend on other factors not included in the data, such as customer budget, competitor offers, contract negotiations, service satisfaction, management decisions, or future business plans.

Logistic Regression is also a simple baseline model. It may not capture more complex patterns in the data. Future work could compare Logistic Regression with more advanced models such as Decision Tree, Random Forest, Support Vector Machine, or Gradient Boosting.

---

## Responsible AI Reflection

This model should be used responsibly as a decision-support tool.

The company should not use the model to unfairly ignore, exclude, or deprioritize customers. Human judgment is still important when making sales, support, pricing, or customer relationship decisions.

Before using this type of model in a real business environment, the company should test it further, monitor performance, check for bias, and ensure that predictions are used fairly and responsibly.

---

## Files Included

```text
Assignment_2_End_to_End_ML_Pipeline.ipynb
business_account_upgrade_prediction_dataset.csv
README.md
```

Optional supporting files may include:

```text
outputs/
```

The `outputs` folder contains charts generated during the notebook, such as target distribution charts and confusion matrix visualizations.

---

## How to Run the Notebook

1. Download or clone this repository.
2. Open the notebook file:

```text
Assignment_2_End_to_End_ML_Pipeline.ipynb
```

3. Make sure the dataset file is saved in the same folder as the notebook:

```text
business_account_upgrade_prediction_dataset.csv
```

4. Run the notebook from top to bottom.

The notebook uses Python libraries such as:

```text
pandas
matplotlib
scikit-learn
```

---

## Final Conclusion

This project completed an end-to-end machine learning pipeline for predicting business account upgrades using a Logistic Regression baseline model.

The workflow included business understanding, data loading, data inspection, data cleaning, missing value handling, feature and target separation, train-test split, preprocessing, model training, prediction, evaluation, result interpretation, limitation discussion, and responsible AI reflection.

Overall, the project demonstrates how a structured machine learning pipeline can transform business data into a practical prediction model that supports data-driven business decision-making.

