# Assignment 4: Decision Tree Model and Business Interpretation

## Course

MBAI 5310G - AI Programming

## Project Title

FreshBasket Subscription Grocery Delivery: Customer Churn Prediction

## Business Problem

FreshBasket is a subscription-based grocery delivery service. The business wants to identify customers who are likely to cancel or not renew their subscription. Early identification can help the company take retention actions such as customer support follow-up, delivery issue investigation, app engagement reminders, or targeted offers.

## Dataset Used

The dataset used is `freshbasket_customer_churn_dataset.xlsx`.

Each row represents one FreshBasket customer. The dataset includes customer profile, region, subscription, payment, delivery, spending, service-quality, discount, engagement, satisfaction, and churn information.

## Target Variable

The target variable is `Churned`.

* `Yes` = customer churned
* `No` = customer did not churn

## Machine Learning Model

The model used is a `DecisionTreeClassifier`.

The notebook uses a preprocessing pipeline with:

* Median imputation for numerical missing values
* Most frequent value imputation for categorical missing values
* One-hot encoding for categorical variables
* Decision Tree classifier with controlled depth and leaf size

## Main Evaluation Results

| Metric            | Score  | Percentage |
| ----------------- | ------ | ---------- |
| Accuracy          | 0.7262 | 72.62%     |
| Precision for Yes | 0.5000 | 50.00%     |
| Recall for Yes    | 0.6087 | 60.87%     |
| F1-score for Yes  | 0.5490 | 54.90%     |
| Training Accuracy | 0.7560 | 75.60%     |
| Testing Accuracy  | 0.7262 | 72.62%     |
| Accuracy Gap      | 0.0298 | 2.98%      |

## Confusion Matrix

| Actual / Predicted | Predicted No | Predicted Yes |
| ------------------ | ------------ | ------------- |
| Actual No          | 47           | 14            |
| Actual Yes         | 9            | 14            |

## Key Business Insights

The most important features in the Decision Tree model included satisfaction score, monthly spend, delivery issues, app engagement score, membership length, discount use, customer service tickets, average order value, and region-related features.

From a business perspective, recall for the `Yes` class is especially important because a false negative means FreshBasket may miss a customer who is likely to churn. False positives may create unnecessary retention costs, but false negatives may lead to lost recurring revenue.

## One Limitation

The dataset is synthetic and simplified. It may not fully represent real customer behaviour, seasonal grocery demand, competitor pricing, delivery constraints, income differences, or personal reasons for cancellation. Therefore, the model should support business judgment rather than replace it.

## How to Run the Notebook

1. Download or clone this repository.
2. Keep `FreshBasket_Decision_Tree_Assignment_Assignment4.ipynb` and `freshbasket_customer_churn_dataset.xlsx` in the same folder.
3. Open the notebook in Jupyter Notebook, JupyterLab, or Google Colab.
4. Run all cells from top to bottom.
5. The generated charts and result files will be saved in the `outputs/` folder.

## Files Included

* `FreshBasket_Decision_Tree_Assignment_Assignment4.ipynb`
* `FreshBasket_Assignment4_Final_Report.docx`
* `freshbasket_customer_churn_dataset.xlsx`
* `business_plan_freshbasket_customer_churn.docx`
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
  ::: 
