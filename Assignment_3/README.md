# Assignment 3: Classification Models and Evaluation Metrics

## Logistic Regression vs SVM for Business Account Upgrade Prediction

## 1. Project Overview

This project trains and compares two classification models to predict whether a business account is likely to upgrade its account.

The goal of the project is not only to train machine learning models, but also to evaluate their performance using classification metrics and interpret the results from a business perspective.

The two models compared in this notebook are:

* Logistic Regression
* Support Vector Machine (SVM)

The model results can help a business identify accounts that may be suitable for sales follow-up, account review, product demonstrations, training support, or targeted upgrade campaigns.

---

## 2. Business Problem

Many businesses offer different account plans or service levels. Some customers continue with their current plan, while others upgrade to a higher-value account.

The business problem in this project is to predict whether a business account is likely to upgrade.

The key business question is:

**Can the company use account, usage, revenue, support, sales, and training information to predict whether a business account will upgrade?**

This prediction is useful because it can help the business prioritize accounts that may be more likely to upgrade and reduce missed sales opportunities.

---

## 3. Machine Learning Objective

This is a supervised binary classification problem.

The target variable is:

**`Upgraded_Account`**

The target variable has two possible classes:

| Class | Meaning                              |
| ----- | ------------------------------------ |
| Yes   | The business account upgraded        |
| No    | The business account did not upgrade |

The model uses business account information as input features and predicts whether the account belongs to the `Yes` or `No` class.

---

## 4. Dataset Used

The dataset used in this project is:

**`business_account_upgrade_prediction_dataset.xls`**

The dataset contains business account information, including company characteristics, revenue, account activity, support tickets, sales contact, product usage, monthly fee, training participation, and account upgrade status.

The `Account_ID` column was removed before model training because it is only an identifier and does not provide meaningful predictive information.

---

## 5. Input Features

The input features used by the models include:

* Company size
* Industry
* Annual revenue
* Monthly transactions
* Current plan
* Account age in months
* Support tickets
* Sales contacted
* Product usage score
* Monthly fee
* Training attended

The target variable `Upgraded_Account` was separated from the input features before model training.

---

## 6. Data Preparation

The notebook follows a structured machine learning workflow:

1. Loaded the dataset.
2. Inspected the dataset structure.
3. Checked rows, columns, data types, missing values, and duplicates.
4. Removed duplicate records.
5. Reviewed missing values after cleaning.
6. Defined input features `X` and target variable `y`.
7. Split the data into training and testing sets.
8. Applied preprocessing using a pipeline.
9. Trained Logistic Regression.
10. Trained SVM.
11. Evaluated both models using classification metrics.
12. Compared model performance.
13. Interpreted the results from a business perspective.

Missing values were handled inside the preprocessing pipeline. Numerical missing values were handled using median imputation, while categorical missing values were handled using the most frequent value. This helps avoid data leakage because preprocessing is fitted on the training data and then applied to the testing data.

---

## 7. Preprocessing

The notebook uses preprocessing before training the models.

Numerical features were processed using:

* Median imputation
* Standard scaling

Categorical features were processed using:

* Most frequent value imputation
* One-hot encoding

Scaling was included because Logistic Regression and SVM can be affected by differences in feature scale.

---

## 8. Models Used

Two classification models were trained and compared.

### Logistic Regression

Logistic Regression was used as a simple and interpretable baseline classification model.

### Support Vector Machine

SVM was used as a comparison model. SVM can create strong decision boundaries and is useful for comparing performance with Logistic Regression.

Both models were trained using the same training data and evaluated using the same testing data.

---

## 9. Model Evaluation Metrics

Both models were evaluated using the following classification metrics:

* Confusion matrix
* Accuracy
* Precision
* Recall
* F1-score

These metrics were used because accuracy alone may not fully explain model performance, especially when the target classes are not perfectly balanced.

---

## 10. Model Results

### Logistic Regression Results

| Metric            |    Score |
| ----------------- | -------: |
| Accuracy          | 0.770270 |
| Precision for Yes | 0.454545 |
| Recall for Yes    | 0.312500 |
| F1-score for Yes  | 0.370370 |

### SVM Results

| Metric            |    Score |
| ----------------- | -------: |
| Accuracy          | 0.824324 |
| Precision for Yes | 0.714286 |
| Recall for Yes    | 0.312500 |
| F1-score for Yes  | 0.434783 |

---

## 11. Model Comparison

Based on the testing results, **SVM performed better overall** than Logistic Regression.

SVM achieved:

* Higher accuracy
* Higher precision for the `Yes` class
* Same recall for the `Yes` class
* Higher F1-score for the `Yes` class

Although both models had the same recall for the `Yes` class, SVM had better precision and F1-score. This means SVM made fewer incorrect `Yes` predictions and provided a better overall balance between precision and recall.

Therefore, **SVM is selected as the stronger model in this notebook**.

---

## 12. Business Interpretation

From a business perspective, the `Yes` class is important because it represents accounts that are likely to upgrade.

For this project, **recall for the `Yes` class is especially important** because the business wants to identify as many actual upgrade opportunities as possible.

A false positive means the model predicts that an account will upgrade, but the account actually does not upgrade. In business terms, this may lead to unnecessary sales follow-up or wasted marketing effort.

A false negative means the model predicts that an account will not upgrade, but the account actually does upgrade. In business terms, this is more serious because the business may miss a real upgrade opportunity.

Because both models have relatively low recall for the `Yes` class, the business should not rely only on the model to identify all upgrade opportunities.

---

## 13. Limitation and Possible Bias

One limitation of the model is that it depends only on the available dataset. The dataset may not include all factors that influence account upgrades, such as customer budget, competitor offers, contract timing, customer satisfaction, or strategic business needs.

Another limitation is that the `Yes` class is smaller than the `No` class. This may make it harder for the models to correctly identify upgraded accounts.

A possible bias may also exist if some industries, company sizes, or account types are overrepresented or underrepresented in the dataset.

---

## 14. Why Human Judgment Is Still Needed

Human judgment is still important because model predictions are not guaranteed to be correct.

The model can identify patterns in the dataset, but it cannot fully understand customer context, business relationships, contract negotiations, or future customer plans.

Sales and customer success teams should use the model as a decision-support tool, not as the only basis for action. Human review should be used before making final business decisions.

---

## 15. Repository Contents

This repository includes:

* Completed Jupyter Notebook
* Dataset file
* README file
* Outputs folder with generated charts from the notebook

Suggested repository structure:

```text
Assignment_3/
│
├── Assignment_3_Redrafted_Classification_Models_and_Evaluation_Metrics.ipynb
├── business_account_upgrade_prediction_dataset.xls
├── README.md
└── outputs/
    ├── comparison_logistic_regression_vs_svm.png
    ├── logistic_regression_confusion_matrix.png
    ├── missing_values_by_column.png
    ├── model_comparison_metrics.png
    ├── model_comparison_results.png
    ├── number_of_unique_values_in_each_categorical_feature.png
    ├── numerical_vs_categorical_features.png
    ├── svm_confusion_matrix.png
    ├── target_variable_distribution_after_cleaning.png
    ├── target_variable_distribution_before_cleaning.png
    ├── training_set_testing_set_size.png
    └── training_vs_testing_accuracy.png
```

```

---

## 16. How to Run the Notebook

1. Download or clone this repository.
2. Open the Jupyter Notebook.
3. Make sure the dataset file is in the same folder as the notebook.
4. Run all cells from top to bottom.
5. Review the model results, confusion matrices, charts, and business interpretation.

---

## 17. Final Conclusion

This project compared Logistic Regression and SVM classification models for predicting business account upgrades.

The SVM model performed better overall, with a testing accuracy of **82.43%**, precision for the `Yes` class of **71.43%**, recall for the `Yes` class of **31.25%**, and F1-score for the `Yes` class of **43.48%**.

The Logistic Regression model was useful as a baseline model, but SVM provided stronger overall testing performance.

However, both models had low recall for the `Yes` class, meaning they missed many actual upgraded accounts. Therefore, the model should be used as a decision-support tool together with human judgment, business knowledge, and sales team review.
