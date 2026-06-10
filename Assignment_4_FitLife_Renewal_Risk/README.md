# Assignment 4: Decision Tree Model and Business Interpretation

## Course

MBAI 5310G - AI Programming

## Project Title

FitLife Studio Analytics: Membership Renewal Risk Prediction

## Business Problem

FitLife Studio is a fitness subscription business that depends on recurring membership renewals. The business wants to identify members who are at risk of not renewing their membership. Early identification can help FitLife take proactive retention actions such as personalized class suggestions, renewal reminders, service follow-up, billing support, or targeted membership offers.

## Dataset Used

The dataset used is `fitlife_membership_renewal_risk_dataset.xlsx`.

Each row represents one FitLife Studio member. The dataset includes demographic details, membership information, engagement behaviour, app usage, satisfaction indicators, complaint history, payment issues, renewal communication, and renewal-risk information.

## Target Variable

The target variable is `At_Risk_Not_Renewing`.

* `Yes` = member is at risk of not renewing
* `No` = member is not currently considered high risk

## Machine Learning Model

The model used is a `DecisionTreeClassifier`.

The notebook uses a preprocessing pipeline with:

* Median imputation for numerical missing values
* Most frequent value imputation for categorical missing values
* One-hot encoding for categorical variables
* Decision Tree classifier with controlled tree depth

## Main Evaluation Results

| Metric            |  Score | Percentage |
| ----------------- | -----: | ---------: |
| Accuracy          | 0.7439 |     74.39% |
| Precision for Yes | 0.7200 |     72.00% |
| Recall for Yes    | 0.5625 |     56.25% |
| F1-score for Yes  | 0.6316 |     63.16% |
| Training Accuracy | 0.7805 |     78.05% |
| Testing Accuracy  | 0.7439 |     74.39% |
| Accuracy Gap      | 0.0366 |      3.66% |

## Confusion Matrix

| Actual / Predicted | Predicted No | Predicted Yes |
| ------------------ | -----------: | ------------: |
| Actual No          |           43 |             7 |
| Actual Yes         |           14 |            18 |

## Key Business Insights

The most important features in the Decision Tree model included average weekly visits, classes per month, monthly contract type, satisfaction score, renewal reminder status, basic membership type, payment issues, premium membership type, app login activity, and age.

From a business perspective, recall for the `Yes` class is especially important because a false negative means FitLife may miss a member who is actually at risk of not renewing. False positives may create unnecessary staff work or retention-offer costs, but false negatives may lead to preventable membership loss and reduced recurring revenue.

## One Limitation

The dataset is synthetic and relatively small. It may not fully represent all real reasons why members renew or do not renew. Real renewal decisions may be affected by relocation, health, family responsibilities, work schedules, transportation, competitor offers, personal preferences, or financial constraints. Therefore, the model should support business judgment rather than replace it.

## How to Run the Notebook

1. Download or clone this repository.
2. Keep `FitLife_Decision_Tree_Assignment_Assignment4.ipynb` and `fitlife_membership_renewal_risk_dataset.xlsx` in the same folder.
3. Open the notebook in Jupyter Notebook, JupyterLab, or Google Colab.
4. Run all cells from top to bottom.
5. The generated charts and result files will be saved in the `outputs/` folder.

## Files Included

* `FitLife_Decision_Tree_Assignment_Assignment4.ipynb`
* `FitLife_Assignment4_Final_Report.docx`
* `fitlife_membership_renewal_risk_dataset.xlsx`
* `business_plan_fitlife_membership_renewal.pdf`
* `README.md`
* `outputs/` folder containing model charts and result tables

## Outputs Generated

* Target variable distribution chart
* Missing values chart
* Categorical unique values chart
* Training/testing set size chart
* Actual vs predicted class counts chart
* Evaluation metrics chart
* Confusion matrix chart
* Top 10 feature importance chart
* Training vs testing accuracy chart
* Decision Tree visualization
* Evaluation result CSV files
* Feature importance CSV file
* Overfitting summary CSV file
  ::: 

Repository structure:

```text
Assignment_4_FitLife_Renewal_Risk/
│
├── FitLife_Decision_Tree_Assignment_Assignment4.ipynb
├── fitlife_membership_renewal_risk_dataset.xlsx
├── business_plan_fitlife_membership_renewal.pdf
├── FitLife_Assignment4_Final_Report.pdf
├── README.md
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
