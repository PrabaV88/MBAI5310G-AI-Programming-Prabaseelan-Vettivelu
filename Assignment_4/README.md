# FitLife Studio Analytics: Membership Renewal Risk Prediction

## Decision Tree Model and Business Interpretation Based on a Business Plan

## 1. Project Overview

This project develops a **Decision Tree classification model** to predict whether a FitLife Studio member is at risk of not renewing their membership.

FitLife Studio is a fitness subscription business that depends on recurring membership renewals. Member retention is therefore an important business priority. The purpose of this project is not only to build a machine learning model, but also to interpret the model results from a business perspective.

The model can help FitLife Studio identify members who may require proactive retention support before they fail to renew.

## Key Results

- Training Accuracy: **78.05%**
- Testing Accuracy: **74.39%**
- Precision for Yes: **72.00%**
- Recall for Yes: **56.25%**
- F1-Score for Yes: **63.16%**
- Accuracy Difference: **3.66 percentage points**
- The model does **not** show strong signs of overfitting.

---

## 2. Business Problem

The main business problem is **membership churn**.

Some members may become less engaged over time by visiting the studio less often, attending fewer classes, using the app less frequently, reporting lower satisfaction, experiencing payment issues, or not responding to renewal reminders. These behaviours may indicate that a member is at risk of not renewing their membership.

The key business question is:

**Can FitLife Studio predict whether a member is at risk of not renewing their membership using available member information, engagement data, satisfaction indicators, payment history, and membership details?**

---

## 3. Machine Learning Objective

The objective of the machine learning model is to classify each member into one of two categories:

| Class | Meaning |
| ----- | ------- |
| Yes | The member is at risk of not renewing |
| No | The member is not currently considered high risk |

This is a **supervised binary classification problem** because the target variable has two possible class labels.

---

## 4. Dataset Used

The dataset used in this project is:

**`fitlife_membership_renewal_risk_dataset.xlsx`**

The dataset contains information about FitLife Studio members, including demographic details, membership information, engagement behaviour, satisfaction indicators, payment issues, communication history, and renewal-risk status.

### Dataset Size

| Dataset Version | Rows | Columns |
| --------------- | ---: | ------: |
| Original dataset | 416 | 21 |
| Cleaned dataset | 410 | 21 |

Duplicate rows were removed during data cleaning. The number of columns remained the same because duplicate removal affected only repeated member records, not the variables included in the dataset.

---

## 5. Target Variable

The target variable is:

**`At_Risk_Not_Renewing`**

This variable indicates whether a member is at risk of not renewing their membership.

| Class | Meaning |
| ----- | ------- |
| Yes | The member is at risk of not renewing |
| No | The member is not currently considered high risk |

---

## 6. Input Features

The input features used by the model include:

- Age
- Gender
- Membership type
- Monthly fee
- Months as member
- Contract type
- Average weekly visits
- Classes per month
- Personal training
- App login days in the last 30 days
- Payment issues in the last 6 months
- Satisfaction score
- Complaint count in the last 3 months
- Distance from studio
- Last renewal discount used
- Renewal reminder sent
- Corporate plan
- Season
- Referral source

The `Member_ID` column was removed before model training because it is only an identifier and does not provide meaningful business information for predicting renewal risk.

---

## 7. Data Preparation

The following data preparation steps were completed:

1. Loaded the dataset into pandas.
2. Inspected the dataset structure.
3. Checked the number of rows and columns.
4. Checked column names and data types.
5. Checked missing values and duplicate rows.
6. Removed duplicate rows.
7. Reviewed missing values after duplicate removal.
8. Created a missing-value handling strategy.
9. Separated input features and target variable.
10. Removed the ID column from the model input features.
11. Split the dataset into training and testing sets.
12. Applied preprocessing using imputation and one-hot encoding.
13. Trained a Decision Tree classification model.
14. Evaluated the model using classification metrics, confusion matrix, and feature importance.

---

## 8. Missing Value Handling

Missing values were reviewed after duplicate rows were removed.

| Column | Data Type | Missing Values | Planned Method | Handling Location |
| ------ | --------- | -------------: | -------------- | ----------------- |
| Avg_Weekly_Visits | Numerical | 5 | Median | Inside preprocessing pipeline |
| Classes_Per_Month | Numerical | 8 | Median | Inside preprocessing pipeline |
| Satisfaction_Score | Numerical | 9 | Median | Inside preprocessing pipeline |
| Referral_Source | Categorical | 7 | Most frequent value | Inside preprocessing pipeline |

Missing values were **not filled directly in the full dataset before the train-test split**. Instead, missing-value handling was completed inside the preprocessing pipeline.

Numerical missing values were handled using **median imputation**. Categorical missing values were handled using **most frequent value imputation**. This is a stronger machine learning approach because the preprocessing transformer is fitted on the training data and then applied to the testing data.

The target variable was not filled because it is the outcome the model is trying to predict.

---

## 9. Preprocessing

The preprocessing step prepared the training and testing data for the Decision Tree model.

- Numerical features were imputed using the median.
- Categorical features were imputed using the most frequent value.
- Categorical variables were converted into numerical columns using one-hot encoding.
- Numerical variables were not scaled because Decision Tree models do not require feature scaling.

The preprocessing transformer was fitted on the training data and then applied to the testing data. This helps avoid data leakage.

---

## 10. Model Used

The model used in this project is a:

**Decision Tree Classifier**

The model was created using:

```python
DecisionTreeClassifier(max_depth=4, random_state=42)
```

The `max_depth=4` setting was used to keep the tree reasonably simple and interpretable. This helps reduce the risk of overfitting and makes the model easier to explain from a business perspective.

---

## 11. Model Evaluation Results

The Decision Tree model was evaluated using the testing data.

| Metric | Score |
| ------ | ----: |
| Accuracy | 0.743902 |
| Precision for Yes | 0.720000 |
| Recall for Yes | 0.562500 |
| F1-Score for Yes | 0.631579 |

### Interpretation of Evaluation Metrics

The model achieved a testing accuracy of approximately **74.39%**, meaning it correctly classified about 74% of members in the testing dataset.

Precision for the `Yes` class was **72.00%**, meaning that when the model predicted a member as at risk, it was correct 72% of the time.

Recall for the `Yes` class was **56.25%**, meaning that the model identified just over half of the actual at-risk members.

The F1-score for the `Yes` class was approximately **63.16%**, showing moderate performance when balancing precision and recall.

For this business problem, **recall for the Yes class is especially important** because missing at-risk members may reduce FitLife Studio’s opportunity to take proactive retention action.

---

## 12. Training vs Testing Accuracy

| Evaluation Set | Accuracy |
| -------------- | -------: |
| Training Set | 0.780488 |
| Testing Set | 0.743902 |

The difference between training accuracy and testing accuracy was approximately **0.036585**, or **3.66 percentage points**.

This difference is relatively small. Therefore, the model does not show strong signs of overfitting. The model appears to learn useful patterns from the training data while still performing reasonably well on unseen testing data.

---

## 13. Confusion Matrix

|            | Predicted No | Predicted Yes |
| ---------- | -----------: | ------------: |
| Actual No  | 43 | 7 |
| Actual Yes | 14 | 18 |

### Confusion Matrix Interpretation

The model correctly predicted **43 members** as not at risk. These are true negatives.

The model correctly predicted **18 members** as at risk. These are true positives.

The model incorrectly predicted **7 members** as at risk when they were not actually at risk. These are false positives.

The model incorrectly predicted **14 members** as not at risk when they were actually at risk. These are false negatives.

In the FitLife Studio business context, false negatives are especially important because they represent members who were actually at risk but were missed by the model. These members may not receive timely retention support.

---

## 14. Feature Importance

The Decision Tree model identified the following top 10 important features:

1. `Avg_Weekly_Visits`
2. `Classes_Per_Month`
3. `Contract_Type_Monthly`
4. `Satisfaction_Score`
5. `Renewal_Reminder_Sent_Yes`
6. `Membership_Type_Basic`
7. `Payment_Issues_Last_6_Months`
8. `Membership_Type_Premium`
9. `App_Login_Days_Last_30`
10. `Age`

These features suggest that renewal risk is strongly connected to member engagement, membership structure, satisfaction, communication, payment experience, app activity, and age.

Some features, such as contract type and membership type categories, were created through one-hot encoding. This means the original categorical variables were converted into separate binary features before training the model.

---

## 15. Key Business Insights

The model results provide several useful business insights for FitLife Studio.

### Member Engagement

Average weekly visits, classes per month, and app login days were important predictors. Members who visit less often, attend fewer classes, or use the app less frequently may have a higher risk of not renewing.

FitLife Studio can monitor engagement patterns and contact members whose participation declines.

### Membership Structure

Monthly contract type and membership type were important predictors. Monthly members may have more flexibility to stop renewing compared with members on longer-term contracts.

FitLife Studio can design different retention strategies for monthly, basic, standard, premium, student, six-month, and annual members.

### Satisfaction

Satisfaction score was an important predictor. Lower satisfaction may indicate that a member is unhappy with the service, facilities, class options, or overall membership value.

FitLife Studio can use satisfaction scores to identify members who may need service recovery or personalized follow-up.

### Renewal Communication

Renewal reminder status was useful in the model. This suggests that communication may influence renewal behaviour.

FitLife Studio can improve its reminder strategy by sending timely renewal messages through email, app notifications, phone calls, or in-person follow-ups.

### Payment Issues

Payment issues in the last six months were also important. Payment problems may create inconvenience for members and may indicate billing difficulties or financial concerns.

FitLife Studio can provide billing support before the renewal period to reduce friction and improve the chance of renewal.

---

## 16. Business Interpretation

The Decision Tree model performed reasonably well for a first business classification model. A testing accuracy of approximately **74.39%** suggests that the model can correctly classify a meaningful portion of members.

However, the model does not identify all at-risk members. The recall score of **56.25%** means that some at-risk members are missed.

Since FitLife Studio’s goal is to reduce membership churn, the model should be used as a **screening tool** rather than a final decision-making system.

For this business problem, **recall for the Yes class is the most important metric** because FitLife Studio wants to identify as many truly at-risk members as possible before they fail to renew.

A false negative is more costly than a false positive because a missed at-risk member may not receive timely retention support.

---

## 17. Limitation and Possible Bias

One limitation of the model is that it is based only on the available dataset. The dataset may not include all reasons why a member chooses not to renew. For example, a member may leave because of relocation, personal schedule changes, family reasons, health concerns, competitor offers, or financial constraints.

Another limitation is that the dataset is relatively small. With more member records, the model may learn stronger and more reliable patterns.

A possible bias may also exist if certain groups of members are underrepresented in the dataset. If the dataset does not reflect all types of FitLife Studio members fairly, the model’s predictions may be less accurate for some groups.

---

## 18. Why Human Judgment Is Still Needed

Human judgment should still be used when making business decisions based on the model results.

The model can identify patterns in the dataset, but it cannot fully understand personal circumstances. For example, a member may reduce visits temporarily because of work, travel, illness, family responsibilities, or schedule conflicts. The model may interpret this as risk, even if the member still intends to renew.

FitLife Studio managers and staff should use the model as a decision-support tool. They should combine the model’s prediction with customer service knowledge, member communication history, and professional judgment.

The model should support better decisions, not replace human decision-making.

---

## 19. Repository Contents

This repository includes:

- Completed Jupyter Notebook
- Dataset file
- README file
- Business interpretation report
- Generated output charts from the notebook
- Model results, charts, and business interpretation included in the notebook and report

Repository structure:

```text
Assignment_4/
│
├── FitLife_Decision_Tree_Assignment_Assignment4.ipynb
├── fitlife_membership_renewal_risk_dataset.xlsx
├── README.md
├── FitLife_Assignment4_Final_Report.pdf
└── outputs/
    ├── actual_vs_predicted_class_counts.png
    ├── categorical_unique_values.png
    ├── decision_tree_confusion_matrix.png
    ├── decision_tree_evaluation_metrics.png
    ├── decision_tree_evaluation_results.csv
    ├── decision_tree_feature_importance.csv
    ├── decision_tree_visualization.png
    ├── missing_value_handling_plan.csv
    ├── missing_values_by_column.png
    ├── model_results_summary.csv
    ├── overfitting_summary.csv
    ├── target_class_distribution.png
    ├── target_distribution_after_cleaning.png
    ├── top_10_feature_importance.png
    └── training_testing_accuracy_comparison.png
```

---

## 20. How to Run the Notebook

1. Download or clone this repository.
2. Open the Jupyter Notebook.
3. Make sure the dataset file is in the same folder as the notebook.
4. Run all cells from top to bottom.
5. Review the generated charts, tables, model results, and business interpretation.

---

## 21. Final Conclusion

This project shows how a Decision Tree classification model can support FitLife Studio’s membership renewal-risk prediction.

The model achieved approximately **74.39% testing accuracy**, with **72.00% precision**, **56.25% recall**, and **63.16% F1-score** for the at-risk class.

The model does not show strong signs of overfitting because the difference between training and testing accuracy is relatively small.

The most important features included average weekly visits, classes per month, monthly contract type, satisfaction score, renewal reminders, basic membership type, payment issues, premium membership type, app login activity, and age.

From a business perspective, the model can help FitLife Studio identify members who may require proactive retention support. However, because the model misses some actual at-risk members, it should be used together with human judgment and business knowledge.
