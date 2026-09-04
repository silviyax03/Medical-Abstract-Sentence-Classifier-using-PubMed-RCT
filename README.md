# Medical Abstract Sentence Classifier using PubMed RCT

## 📌 Project Overview

The **Medical Abstract Sentence Classifier** is an NLP-based machine learning project that classifies individual sentences from medical research abstracts into predefined sections.

The project uses the **PubMed 20k RCT dataset** and predicts one of five categories:

- BACKGROUND
- OBJECTIVE
- METHODS
- RESULTS
- CONCLUSIONS

The project compares traditional machine learning with deep learning approaches and deploys the selected model using **Streamlit**.

---

## 🎯 Problem Statement

Medical research abstracts contain different types of information such as study background, objectives, methodology, results, and conclusions.

Automatically identifying the role of each sentence can help organize and analyze large volumes of biomedical literature.

This project aims to build an NLP classification system that automatically assigns the appropriate section label to each sentence in a medical abstract.

---

## 🎯 Objectives

- Load and structure the PubMed RCT dataset.
- Perform data quality checks.
- Prepare sentence-level text data for classification.
- Extract text features using TF-IDF.
- Build a Logistic Regression baseline model.
- Build and evaluate Text-CNN and BiLSTM models.
- Compare model performance using Accuracy and Macro F1.
- Evaluate the final model on unseen test data.
- Create a sentence-level prediction function.
- Deploy the final model using Streamlit.

---

## 📊 Dataset

### PubMed 20k RCT

The project uses the **PubMed 20k RCT dataset**, which contains sentences extracted from biomedical research abstracts.

Each sentence is associated with a section label.

### Target Classes

| Label | Description |
|---|---|
| BACKGROUND | Provides background or context for the study |
| OBJECTIVE | Describes the purpose or objective of the study |
| METHODS | Describes the study methodology |
| RESULTS | Presents study findings or results |
| CONCLUSIONS | Provides the conclusion or interpretation |

---

## 🛠️ Technologies Used

### Programming Language

- Python

### Data Processing

- Pandas
- NumPy

### Machine Learning

- Scikit-learn
- TF-IDF
- Logistic Regression

### Deep Learning

- TensorFlow / Keras
- TextVectorization
- Text-CNN
- BiLSTM

### Model Evaluation

- Accuracy
- Macro F1 Score
- Precision
- Recall
- Classification Report
- Confusion Matrix

### Deployment

- Streamlit
- Joblib
- Cloudflare Tunnel

---

## 🔄 Project Workflow

```text
PubMed RCT Dataset
        ↓
Data Loading
        ↓
Data Structuring
        ↓
Data Quality Checks
        ↓
Train / Validation / Test Split
        ↓
       ┌─────────────────────┐
       │                     │
       ↓                     ↓
    TF-IDF             TextVectorization
       ↓                     ↓
Logistic Regression    ┌─────┴─────┐
                       ↓           ↓
                   Text-CNN      BiLSTM
                       ↓           ↓
                       └─────┬─────┘
                             ↓
                     Model Comparison
                             ↓
                    Final Model Selection
                             ↓
                    Unseen Test Evaluation
                             ↓
                    Streamlit Deployment
```

---

## 🧹 Data Preprocessing & Data Quality Checks

### 1. Data Loading & Structuring

The raw PubMed RCT dataset was loaded and parsed into a structured Pandas DataFrame.

The following fields were extracted:

- `abstract_id`
- `sentence`
- `label`

### 2. Data Quality Checks

The dataset was checked for:

- Dataset shape and structure
- Missing/null values
- Duplicate records
- Class distribution
- Presence of the five target classes

### 3. Data Preparation

- Sentence text was used as the input variable.
- Section label was used as the target variable.
- Labels were encoded for model training.
- Training, validation, and test datasets were maintained separately.

---

## 🔤 TF-IDF Feature Extraction

TF-IDF (**Term Frequency-Inverse Document Frequency**) was used to convert text sentences into numerical feature vectors.

The TF-IDF vectorizer was:

1. Fitted using the training data.
2. Used to transform validation data.
3. Used to transform test data.

The resulting sparse numerical feature matrices were provided as input to the Logistic Regression model.

---

## 🤖 Models Used

### 1. TF-IDF + Logistic Regression

Logistic Regression was used as the traditional machine learning baseline.

**Workflow:**

```text
Sentence
   ↓
TF-IDF Vectorization
   ↓
Numerical Feature Vector
   ↓
Logistic Regression
   ↓
Predicted Label
```

---

### 2. Text-CNN

A Text-CNN model was developed using:

- TextVectorization
- Embedding layer
- Conv1D layer
- Dense layer
- Dropout
- Output layer

**Configuration:**

- Vocabulary size: `50,000`
- Sequence length: `50`
- Embedding dimension: `128`
- Conv1D filters: `128`
- Kernel size: `5`
- Training epochs: `5`

---

### 3. BiLSTM

A Bidirectional LSTM model was developed to capture contextual information from both directions of a sentence.

**Architecture:**

```text
Text
  ↓
TextVectorization
  ↓
Embedding
  ↓
Bidirectional LSTM
  ↓
Dense
  ↓
Dropout
  ↓
Output
```

**Configuration:**

- Vocabulary size: `50,000`
- Sequence length: `50`
- Embedding dimension: `128`
- Training epochs: `5`

---

## 📈 Model Evaluation

The models were evaluated using:

- Accuracy
- Macro F1 Score
- Precision
- Recall
- Classification Report
- Confusion Matrix

**Macro F1** was considered important because the dataset contains multiple sentence classes, and performance should be evaluated across all classes.

---

## 🏆 Model Comparison

### Validation Performance

| Model | Validation Accuracy | Validation Macro F1 |
|---|---:|---:|
| Text-CNN | 80.72% | 74.00% |
| BiLSTM | 81.40% | 75.07% |
| **TF-IDF + Logistic Regression** | **83.12%** | **76.71%** |

### Final Model

**TF-IDF + Logistic Regression** was selected as the final model because it achieved the best validation performance among the evaluated approaches.

---

## 🧪 Final Test Evaluation

The selected model was evaluated on the unseen test dataset.

### Final Results

- **Test Accuracy:** `82.29%`
- **Test Macro F1:** `75.98%`

### Classification Report

| Class | Precision | Recall | F1 Score |
|---|---:|---:|---:|
| BACKGROUND | 0.66 | 0.66 | 0.66 |
| CONCLUSIONS | 0.76 | 0.75 | 0.75 |
| METHODS | 0.87 | 0.93 | 0.90 |
| OBJECTIVE | 0.71 | 0.53 | 0.61 |
| RESULTS | 0.88 | 0.88 | 0.88 |

The final test evaluation demonstrates that the model can classify unseen medical abstract sentences across the five target categories.

---

## 🔍 Prediction

The trained model can classify individual sentences as well as sentences from a complete abstract.

**Example:**

**Input:**

> The study was conducted to evaluate the effectiveness of the treatment.

**Prediction:**

`OBJECTIVE`

For a complete abstract, the application splits the abstract into individual sentences and predicts a section label for each sentence.

---

## 🎨 Streamlit Application

A Streamlit web application was developed for interactive prediction.

The application allows the user to:

1. Enter or paste a medical abstract.
2. Click **Classify Abstract**.
3. Split the abstract into individual sentences.
4. Predict the category for each sentence.
5. Display each sentence with its predicted label.

The application uses color-coded output for easier interpretation.

### Label Guide

| Label | Meaning |
|---|---|
| BACKGROUND | Study context |
| OBJECTIVE | Study purpose |
| METHODS | Study methodology |
| RESULTS | Study findings |
| CONCLUSIONS | Study conclusion |

---

## 💾 Model Persistence

The trained model and TF-IDF vectorizer were saved using Joblib.

**Files used by the Streamlit application:**

- `logistic_model.pkl`
- `tfidf_vectorizer.pkl`

This allows the application to load the trained components without retraining the model every time it starts.

---

## 📌 Key Takeaways

- The project demonstrates an end-to-end biomedical NLP classification workflow.
- TF-IDF + Logistic Regression provided the strongest validation performance among the evaluated models.
- Text-CNN and BiLSTM were also implemented and compared.
- The final model achieved **82.29% test accuracy** and **75.98% test Macro F1**.
- The trained model was integrated into a Streamlit application for interactive sentence-level classification.

---

## 👩‍💻 Project Workflow Summary

```text
Dataset
   ↓
Data Preprocessing
   ↓
Data Quality Checks
   ↓
TF-IDF Feature Extraction
   ↓
Logistic Regression Baseline
   ↓
Text-CNN & BiLSTM Comparison
   ↓
Model Selection
   ↓
Final Test Evaluation
   ↓
Model Persistence
   ↓
Streamlit Deployment
```

---

## 📜 Conclusion

The Medical Abstract Sentence Classifier successfully demonstrates how Natural Language Processing and machine learning can be applied to automatically categorize sentences in biomedical research abstracts.

The project combines traditional machine learning and deep learning approaches, evaluates their performance using multiple metrics, selects the best-performing approach based on validation results, and provides an interactive Streamlit application for practical demonstration.

---

## 👩‍💻 Author

**Silviya X**  
Medical Abstract Sentence Classifier — Biomedical NLP Project
