# Assignment 5: Clustering and Customer Segmentation

## Course

MBAI 5310G - AI Programming

## Project Title

EventEdge Corporate Training: Participant Segmentation Using K-means Clustering

## Business Problem

EventEdge Corporate Training is a B2B corporate training and workforce development company. The business provides professional development programs to organizations in areas such as Data Analytics, Leadership, Project Management, Customer Experience, Digital Marketing, and AI for Business.

The main business problem is participant dropout. When participants stop attending or fail to complete a paid training course, EventEdge may face lower client satisfaction, reduced renewal rates, wasted coaching capacity, and weaker training outcomes.

This assignment uses unsupervised learning to discover meaningful participant groups based on early engagement, course, support, and business-context features.

## Dataset Used

The dataset used is:

`eventedge_training_dropout_risk_dataset.csv`

Each row represents one participant enrolled in an EventEdge corporate training course. The dataset includes participant, course, engagement, support, and satisfaction-related variables.

Although the dataset includes `High_Dropout_Risk`, this variable is not used as a target variable for K-means clustering. It is used only as a reference outcome to understand the business context after clustering.

## Machine Learning Task

This is an unsupervised learning assignment.

Unlike supervised learning, this assignment does not predict a target variable. Instead, K-means clustering is used to discover hidden participant groups based on selected numerical features.

## Clustering Method

The clustering method used is:

`KMeans`

The notebook follows these main steps:

1. Understand the business problem
2. Import required libraries
3. Load the dataset
4. Inspect the dataset
5. Check missing values and duplicate rows
6. Clean the dataset
7. Review High Dropout Risk distribution as business context
8. Review missing values by column
9. Select useful numerical features for clustering
10. Scale the selected numerical features
11. Apply the Elbow Method
12. Train the final K-means clustering model
13. Add cluster labels back to the dataset
14. Analyze and interpret cluster profiles
15. Visualize the clusters
16. Provide business recommendations
17. Discuss limitations and responsible AI use

## Selected Features for Clustering

Only numerical features useful for clustering are selected. Identifier columns and reference outcome columns are not used for training the clustering model.

`Participant_ID` is excluded because it is only an identifier.

`High_Dropout_Risk` is excluded because this is an unsupervised learning assignment and the model should not use a target label.

The selected numerical features are scaled before applying K-means because K-means is distance-based and can be affected by feature magnitude.

## Elbow Method and Choice of K

The Elbow Method was used to compare inertia values for different numbers of clusters.

The elbow curve does not show a perfectly sharp turning point, but `K = 4` provides a reasonable balance between lower inertia and business interpretability. Four clusters also allow EventEdge to describe participants in practical business language and create meaningful participant segments for marketing and support decisions.

## Final Number of Clusters

The final K-means model uses:

`K = 4`

## Main Cluster Segments

The final clustering model identified four participant segments:

| Cluster | Segment Name                                    |
| ------- | ----------------------------------------------- |
| 0       | Active Short-Course Learners                    |
| 1       | At-Risk Long-Course Low-Engagement Participants |
| 2       | Premium Engaged Long-Course Participants        |
| 3       | Moderate-Engagement Short-Course Participants   |

## Main Business Insights

The clustering results show that EventEdge participants are not all the same. Some participants are highly engaged and satisfied, while others show weaker early engagement, longer course exposure, or lower support signals.

The most valuable segment is likely the Premium Engaged Long-Course Participants because they show stronger engagement and may represent high-value training participants.

The segment needing the most marketing and support attention is the At-Risk Long-Course Low-Engagement Participants group. This group may need early reminders, coaching check-ins, manager support, flexible deadlines, and improved onboarding.

## Business Recommendations

EventEdge can use the clustering results to create more targeted participant support strategies.

Recommended actions include:

* Provide early coaching and reminder support for low-engagement participants.
* Use manager-support reminders for participants who may need workplace encouragement.
* Provide personalized progress messages for moderately engaged participants.
* Maintain premium service and relationship management for highly engaged long-course participants.
* Review long-course participants carefully because longer programs may require milestone-based support.
* Use cluster insights to improve marketing messages, onboarding, course design, and client reporting.

## Visualizations Included

The notebook includes visualizations to support the analysis, such as:

* High Dropout Risk distribution chart
* Missing values by column chart
* Elbow Method plot
* Cluster comparison charts
* Cluster average bar charts
* PCA-based cluster visualization

Each visualization includes a short interpretation explaining what the chart shows and how it supports the business analysis.

## Limitations and Responsible AI Reflection

One limitation of this analysis is that K-means clustering may not always create perfect customer or participant segments. K-means groups observations based on distance, so results can be affected by selected features, scaling, outliers, and the chosen number of clusters.

The dataset is also simplified and may not capture all real-world reasons for participant dropout, such as personal circumstances, workload changes, manager communication, health issues, motivation, or organizational culture.

The clusters should not be used to blame participants or make unfair decisions. For example, a participant in a lower-engagement segment should not automatically be treated negatively. Instead, the cluster should be used to provide helpful support, such as reminders, coaching, flexible deadlines, or manager communication.

Human judgment should still be used because managers and program advisors can consider context that the model cannot fully understand.

## Files Included

```text
Assignment_5_EventEdge_Clustering_Segmentation/
│
├── EventEdge_Assignment5_Clustering_Customer_Segmentation.ipynb
├── eventedge_training_dropout_risk_dataset.csv
├── eventedge_training_dropout_business_plan.docx
├── README.md
└── outputs/
    ├── business_recommendations_by_segment.csv
    ├── categorical_unique_values.png
    ├── cluster_dropout_distribution.csv
    ├── cluster_engagement_averages.png
    ├── cluster_scatter_lms_satisfaction.png
    ├── cluster_sizes.png
    ├── cluster_summary.csv
    ├── data_quality_review.csv
    ├── duplicate_cleaning_summary.csv
    ├── elbow_method.png
    ├── elbow_method_values.csv
    ├── eventedge_clustered_results.csv
    ├── feature_type_summary.csv
    ├── high_dropout_risk_distribution.png
    ├── missing_value_handling_plan.csv
    ├── missing_value_summary.csv
    ├── missing_values_by_column.png
    ├── pca_cluster_visualization.png
    ├── selected_feature_summary.csv
```

## How to Run the Notebook

1. Download or clone this repository.
2. Keep the notebook and dataset in the same folder.
3. Open `EventEdge_Assignment5_Clustering_Customer_Segmentation.ipynb` in Jupyter Notebook, JupyterLab, or Google Colab.
4. Run all cells from top to bottom.
5. The generated charts and CSV files will be saved in the `outputs/` folder.

## Important Note

This assignment is based on unsupervised learning. Therefore, `High_Dropout_Risk` is not used to train the K-means model. It is included only as a reference to help understand the business meaning of the discovered participant segments.
