# Assignment 6: Model Evaluation, Explainability, and Fairness Reflection

## Project Title

**University Advising Appointment Non-Completion Prediction**

## Course

**MBAI 5310G – AI Programming**

## Project Overview

This project evaluates a machine learning classification model for a university advising appointment dataset. The main goal is to predict whether an advising appointment is at risk of **not being completed** so that the advising office can take timely support actions such as sending reminders, confirming attendance, offering rescheduling options, or providing additional student follow-up.

The assignment goes beyond basic model accuracy. It includes model evaluation, confusion matrix interpretation, error analysis, cross-validation, overfitting and underfitting analysis, feature importance, SHAP explainability, LIME explainability, and fairness reflection across student groups.

## Dataset Description

The dataset used in this project is:

```text
university_advising_completion_dataset.csv
```

Each row represents one university advising appointment. The dataset includes student profile information, advising context, appointment booking behavior, previous advising behavior, academic indicators, reminder information, appointment mode, previous advising rating, and appointment completion outcome.

### Dataset Summary

| Item | Value |
|---|---:|
| Original dataset shape | 360 rows × 17 columns |
| Missing values | 6 missing values in `current_gpa` |
| Duplicate records | 0 |
| Original target variable | `appointment_completed` |
| Business target used | `appointment_not_completed` |
| Positive class | Not Completed |
| Problem type | Supervised binary classification |

## Target Variable

The original dataset contains the target column:

```text
appointment_completed
```

For business-risk interpretation, this project creates a new target variable:

```text
appointment_not_completed
```

The positive class is:

```text
1 = Not Completed
```

This framing is useful because the main business concern is identifying appointments that may not be completed and may need reminder or support action before the scheduled advising time.

## Input Features and Removed Columns

The model uses advising-related numerical and categorical features as inputs.

### Numerical Features

```text
booking_lead_days
previous_advising_visits
missed_appointments_last_year
credits_completed
current_gpa
advisor_rating_previous
```

### Categorical Features

```text
student_level
program_area
appointment_type
email_reminder_sent
appointment_mode
```

### Removed or Fairness-Only Columns

| Column | Treatment | Reason |
|---|---|---|
| `appointment_id` | Removed | Identifier only; not meaningful for prediction |
| `appointment_completed` | Removed after target conversion | Original target column |
| `age_group` | Fairness analysis only | Excluded from model input to avoid direct group-based prediction |
| `gender` | Fairness analysis only | Excluded from model input to avoid direct group-based prediction |
| `region` | Fairness analysis only | Excluded from model input to avoid direct group-based prediction |
| `student_age` | Removed | May act as a proxy for `age_group` |

## Model Used

The model used is a:

```text
DecisionTreeClassifier
```

The model is built using a scikit-learn Pipeline with a ColumnTransformer. The preprocessing pipeline includes:

- Median imputation for numerical missing values
- Most-frequent imputation for categorical missing values
- One-hot encoding for categorical variables
- Decision Tree classification model

A pipeline is used to reduce the risk of data leakage because preprocessing is fitted only on the training data and then applied to the testing data.

## Main Evaluation Results

| Metric | Score | Percentage |
|---|---:|---:|
| Accuracy | 0.6944 | 69.44% |
| Precision for Not Completed | 0.5405 | 54.05% |
| Recall for Not Completed | 0.8000 | 80.00% |
| F1-score for Not Completed | 0.6452 | 64.52% |

## Confusion Matrix

| Actual / Predicted | Predicted Completed | Predicted Not Completed |
|---|---:|---:|
| Actual Completed | 30 | 17 |
| Actual Not Completed | 5 | 20 |

### Business Meaning of the Confusion Matrix

| Item | Value | Business Meaning |
|---|---:|---|
| True Negative | 30 | Completed appointments correctly predicted as completed |
| False Positive | 17 | Completed appointments incorrectly predicted as not completed; may cause unnecessary reminders or support |
| False Negative | 5 | Not completed appointments incorrectly predicted as completed; may cause missed intervention opportunities |
| True Positive | 20 | Not completed appointments correctly identified for possible support |

## Main Business Interpretation

The model is designed to help a university advising office identify appointments that are at risk of not being completed. The most important metric for this business problem is **recall for the Not Completed class** because a false negative means the model misses an appointment that may need reminder or support action.

The model achieved **80.00% recall**, meaning it identified most of the not-completed appointments in the test set. This is useful for a student-support context. However, the model also produced **17 false positives**, meaning some students who would have completed their appointments were still flagged as at risk. Therefore, the model should be used as a decision-support tool, not as an automatic decision system.

From a practical advising perspective, predictions should be used to guide helpful outreach such as reminders, appointment confirmation, rescheduling options, or supportive follow-up. The model should not be used to penalize students or make final decisions without human review.

## Explainability Summary

The project uses both SHAP and LIME to explain the Decision Tree model.

- **Feature importance** identifies the variables that contribute most to model splits.
- **SHAP** explains how features influence predictions globally and for an individual record.
- **LIME** explains one selected prediction by showing which feature conditions support or oppose the prediction.

The most important model features include:

- `missed_appointments_last_year`
- `previous_advising_visits`
- `current_gpa`
- `advisor_rating_previous`
- `student_level_First Year`

Feature importance and explainability results should be interpreted as model-behavior insights, not as proof of cause and effect.

## Fairness and Bias Reflection

Fairness analysis was completed for the following group-related columns:

```text
age_group
gender
region
```

For each group column, the notebook reports:

- Number of records in each group
- Actual positive rate
- Predicted positive rate
- Accuracy by group

The fairness results show that model behavior is not identical across all student groups. Because some groups in the test set are relatively small, fairness percentages may be sensitive to a small number of prediction errors. Therefore, the model should be monitored carefully before real use, and advising staff should treat predictions as supportive signals rather than final judgments.

## One Limitation of the Model

One important limitation is the small dataset size. The dataset contains only **360 records**, and the test set contains only **72 records**. This means that subgroup fairness results can change noticeably if only a few predictions are different. Real university advising decisions may also be influenced by factors not included in the dataset, such as transportation issues, financial stress, mental health, work schedules, family responsibilities, or program-specific advising culture.

Because of this, the model should be considered an **early prototype**. It needs more data, further testing, and ongoing fairness monitoring before being used in a real advising environment.

## Files Included

```text
Assignment_6_University_Advising/
│
├── Assignment_6_University_Advising_Model_Evaluation_Explainability_Fairness_REVISED.ipynb
├── Assignment_6_University_Advising_Final_Report.pdf
├── university_advising_completion_dataset.csv
├── README.md
└── outputs/
    ├── actual_vs_predicted_values.csv
    ├── classification_report.csv
    ├── confusion_matrix_values.csv
    ├── confusion_matrix_business_meaning.csv
    ├── cross_validation_results.csv
    ├── decision_tree_evaluation_metrics.csv
    ├── decision_tree_feature_importance.csv
    ├── error_analysis_all_predictions.csv
    ├── error_type_counts.csv
    ├── fairness_summary_by_age_group.csv
    ├── fairness_summary_by_gender.csv
    ├── fairness_summary_by_region.csv
    ├── lime_explanation_table.csv
    ├── shap_individual_record_explanation.csv
    ├── target_distribution.csv
    ├── tree_depth_comparison.csv
    ├── wrong_predictions_table.csv
    ├── target_variable_distribution.png
    ├── missing_values_by_column.png
    ├── training_testing_set_size.png
    ├── decision_tree_evaluation_metrics.png
    ├── decision_tree_confusion_matrix.png
    ├── error_type_counts.png
    ├── cross_validation_accuracy.png
    ├── training_testing_accuracy_by_depth.png
    ├── top_10_feature_importance.png
    ├── shap_summary_plot.png
    ├── shap_individual_prediction.png
    ├── lime_individual_prediction.png
    ├── fairness_metrics_by_age_group.png
    ├── fairness_metrics_by_gender.png
    └── fairness_metrics_by_region.png
```

## How to Run the Notebook

1. Download or clone this repository.
2. Keep the notebook and dataset in the same folder.
3. Make sure the dataset file is named:

```text
university_advising_completion_dataset.csv
```

4. Open the notebook in Jupyter Notebook, JupyterLab, or Google Colab.
5. Run all cells from top to bottom.
6. The generated CSV files and charts will be saved in the `outputs/` folder.

## Required Libraries

The notebook uses the following main Python libraries:

```text
pandas
numpy
matplotlib
scikit-learn
shap
lime
```

If SHAP or LIME is not installed, they can be installed using:

```python
pip install shap lime
```

## Final Recommendation

The Decision Tree model is useful as an early decision-support prototype for identifying advising appointments that may not be completed. It performs well in terms of recall for the Not Completed class, which is important for proactive student support. However, because of false positives, fairness differences across groups, and the small dataset size, the model is not ready for fully automated business use.

The recommended next step is to collect more advising appointment records, compare the Decision Tree with stronger models such as Random Forest or Gradient Boosting, and continue fairness monitoring before using the model in real advising operations.

