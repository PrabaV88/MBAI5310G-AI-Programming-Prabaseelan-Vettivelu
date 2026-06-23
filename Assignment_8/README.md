# Assignment 8: Natural Language Processing Pipeline and Text Classification

## Project Title

**Smart Home Device Support Message Classification**

## Course

**AI Programming / Programming and Data Processing**

## Project Overview

This project builds a complete Natural Language Processing (NLP) pipeline for smart home customer support messages. The goal is to show how raw support text can be cleaned, processed, converted into numerical features, and used to classify each customer message into the correct support category.

The business context is a smart home company called **HomeIQ**. Customers may contact support about Wi-Fi connectivity, installation, security alerts, warranty returns, energy-saving features, or voice assistant issues. A text classification model can help route messages to the correct support team more quickly and reduce manual sorting work.

## Business Problem

HomeIQ receives support messages through channels such as email, chat, web forms, and phone transcripts. Manually reading and classifying every message can delay support routing and increase staff workload.

The business problem is to classify each support message into the correct support category so that:

- Connectivity messages can be routed to technical or network support.
- Security alert messages can be prioritized because of their safety-related nature.
- Warranty return messages can be routed to replacement or returns support.
- Energy-saving messages can be routed to product education or thermostat guidance.
- Voice assistant messages can be routed to platform or integration support.

This assignment is treated as a classroom prototype. The model demonstrates the NLP workflow, but it is not intended to be used as a deployment-ready business system without further validation on real customer support data.

## Dataset

The dataset used in this assignment is:

```text
NLP_Dataset_16_Smart_Home_Device_Support.xlsx
```

Each row represents one smart home support message.

### Dataset Summary

| Item | Value |
|---|---:|
| Rows | 120 |
| Columns | 9 |
| Missing values | 0 in all columns |
| Duplicate full records | 0 |
| Text column | `SupportMessage` |
| Target variable | `SupportCategory` |
| Number of support categories | 6 |

### Main Columns

| Column | Description |
|---|---|
| `SupportID` | Unique identifier for each support record |
| `SupportDate` | Date of the support message or request |
| `Channel` | Customer contact channel, such as email, chat, web form, or phone transcript |
| `City` | Customer city |
| `DeviceType` | Smart home device involved in the message |
| `CustomerSegment` | Customer segment, such as homeowner or renter |
| `SupportMessage` | Raw customer support text used for NLP |
| `SupportCategory` | Target label predicted by the model |
| `IssueSeverity` | Severity indicator useful for support prioritization |

## Target Variable

The target variable is:

```text
SupportCategory
```

The model classifies each support message into one of the following categories:

```text
Connectivity
Energy_Saving
Installation
Security_Alert
Voice_Assistant
Warranty_Return
```

The dataset is balanced, with 20 records in each category.

## NLP Pipeline

The notebook follows a complete NLP workflow:

1. Load and inspect the dataset.
2. Select the main text column and target variable.
3. Clean and preprocess the support messages.
4. Analyze common words and word-frequency patterns.
5. Apply POS tagging and Named Entity Recognition.
6. Convert cleaned text into numerical TF-IDF features.
7. Train a text classification model.
8. Evaluate the model using accuracy, confusion matrix, and classification report.
9. Diagnose why the model achieved 100% accuracy.
10. Provide final business interpretation and limitations.

## Text Preprocessing

The following preprocessing steps were applied to `SupportMessage`:

- Lowercase conversion
- Punctuation removal
- Tokenization
- Stopword removal
- Stemming using Porter Stemmer
- Creation of a cleaned text column

Example:

```text
Original message:
The app did not notify me when the back door opened.

Cleaned text:
app notifi back door open
```

The preprocessing step helps remove low-information words and standardize word forms before modelling.

## Exploratory Text Analysis

The notebook identifies the most frequent cleaned words in the support messages. Common terms include:

```text
homeiq
work
camera
thermostat
app
light
hub
secur
alert
warranti
```

These words show that customers contact HomeIQ about recurring support themes such as device failures, app notifications, security events, thermostat use, and warranty or replacement requests.

## POS Tagging and Named Entity Recognition

The notebook applies POS tagging and NER to selected example records. The selected examples represent different business situations, including:

- Connectivity
- Security alert
- Warranty return

In the executed notebook, NLTK POS tagging and NLTK NER resources were available. A rule-based business entity detector is also included as a backup and supplement for environments where NLTK resources are unavailable.

The analysis helps identify useful business information such as:

- Nouns that refer to products, devices, or locations
- Verbs that describe customer actions or device failures
- Entities such as city names, device names, platforms, and time expressions

## Feature Extraction

The cleaned support messages were converted into numerical features using:

```text
TF-IDF Vectorizer
```

The vectorizer uses:

```text
Unigrams and bigrams
```

The TF-IDF matrix shape was:

```text
120 rows × 276 features
```

Text must be converted into numbers because machine learning models cannot directly process raw words.

## Model Used

The classification model used is:

```text
Logistic Regression
```

Logistic Regression was selected because it works well with sparse TF-IDF text features, supports multi-class classification, trains quickly on small datasets, and is a strong baseline model for text classification.

## Model Evaluation Results

| Metric | Result |
|---|---:|
| Accuracy | 100.00% |
| Precision | 1.00 for every class |
| Recall | 1.00 for every class |
| F1-score | 1.00 for every class |
| Test records | 24 |

The confusion matrix showed all values on the diagonal and no off-diagonal errors. This means the model classified all 24 test messages correctly.

## Diagnostic Review of 100% Accuracy

The 100% accuracy should be interpreted carefully. A diagnostic check was added because perfect accuracy on a six-class text classification problem may indicate an artificially easy dataset.

The diagnostic review found:

| Diagnostic Item | Result |
|---|---|
| Duplicated cleaned-text messages | 75 duplicated cleaned-text messages |
| Percentage of all records | 62.50% |
| Anchor-term pattern | Anchor terms appear almost exclusively in one category |

Examples of strong category-specific anchor terms include:

| Anchor Term | Main Associated Category |
|---|---|
| `alert` | Security_Alert |
| `warranti` | Warranty_Return |
| `return` | Warranty_Return |
| `energi` | Energy_Saving |
| `instal` | Installation |
| `bluetooth` | Connectivity |
| `voic` | Voice_Assistant |

This means the model likely achieved perfect accuracy because the dataset is small, synthetic, templated, and contains strong keyword patterns. Therefore, the result proves that the NLP pipeline works, but it should not be interpreted as evidence that the model is ready for production use.

## Business Interpretation

The model demonstrates that NLP can be used to classify smart home customer support messages into useful business categories. This can support faster message routing, better prioritization, and improved understanding of recurring support themes.

However, the model should be treated as a classroom prototype. Before real business deployment, HomeIQ should retrain and test the model using larger real-world support messages with natural language variation, spelling errors, mixed topics, and messages that do not contain obvious category keywords.

## Limitations

| Limitation | Why It Matters | Recommended Next Step |
|---|---|---|
| Small dataset size | Only 120 records are available | Collect a larger real-world support dataset |
| Synthetic and templated text | Messages are cleaner than real customer messages | Validate using naturally written customer support messages |
| Repeated cleaned-message patterns | Duplicates may make the model memorize phrasing | Remove duplicates or use grouped splitting |
| Obvious category keywords | The model can rely on anchor words | Test messages without obvious keywords |
| Limited real-world language variation | Real messages may contain spelling errors, sarcasm, incomplete sentences, or mixed issues | Monitor performance across channel, city, device type, and customer segment |

## Files Included

```text
Assignment_8_Smart_Home_NLP_Text_Classification/
│
├── Assignment_8_Smart_Home_NLP_Text_Classification.ipynb
├── Assignment_8_Smart_Home_NLP_Final_Report.pdf
├── NLP_Dataset_16_Smart_Home_Device_Support.xlsx
├── README.md
└── outputs/
    ├── actual_vs_predicted_text_classification.csv
    ├── anchor_term_by_category.csv
    ├── class_level_evaluation_summary.csv
    ├── classification_report.csv
    ├── cleaned_text_sample.csv
    ├── confusion_matrix.csv
    ├── confusion_matrix.png
    ├── data_types.csv
    ├── duplicate_records_summary.csv
    ├── duplicated_cleaned_text_examples.csv
    ├── final_business_summary.csv
    ├── missing_values_summary.csv
    ├── ner_examples.csv
    ├── pos_tagging_examples.csv
    ├── target_distribution.csv
    ├── target_distribution.png
    ├── text_preprocessing_examples.csv
    ├── tfidf_feature_sample.csv
    ├── top_20_word_frequency.csv
    └── top_20_word_frequency.png
```

## How to Run the Notebook

1. Download or clone the repository.
2. Open the Assignment 8 folder.
3. Make sure the notebook and Excel dataset are in the same folder.
4. Open the notebook:

```text
Assignment_8_Smart_Home_NLP_Text_Classification.ipynb
```

5. Run all cells from top to bottom.
6. The generated CSV files and charts will be saved in the `outputs/` folder.

## Required Libraries

The notebook uses the following Python libraries:

```text
pandas
numpy
matplotlib
scikit-learn
nltk
openpyxl
```

If required, install missing packages using:

```python
pip install pandas numpy matplotlib scikit-learn nltk openpyxl
```

## Final Recommendation

This project successfully demonstrates an end-to-end NLP pipeline for smart home support message classification. The model achieved 100% accuracy on the classroom dataset, but the diagnostic review shows that the result is mainly due to strong category-specific keywords and repeated cleaned-text patterns.

The recommended next step is to validate the pipeline on a larger and more realistic support-message dataset before considering any automated business use.

