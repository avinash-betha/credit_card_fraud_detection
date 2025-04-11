# Credit Card Fraud Detection Using PySpark and AWS

## Overview
This project focuses on solving the real-world challenge of detecting fraudulent credit card transactions by leveraging scalable, distributed computing and cloud technologies. Built using Apache Spark, AWS EMR, and Athena, the solution processes over 1 million records and applies logistic regression for accurate fraud detection. The system is designed with real-time fraud alerts and practical deployment in mind.

## Objective
To build a high-accuracy, end-to-end machine learning pipeline for detecting fraudulent credit card transactions. This project simulates how financial institutions can reduce fraud-related losses using cloud infrastructure and scalable big data tools.

## Dataset
- Source: [PaySim Synthetic Dataset](https://www.kaggle.com/datasets/ealaxi/paysim1)
- Size: 1M+ transactions
- Format: CSV (ingested into PySpark DataFrame)
- Features:
  - step: Time step of transaction
  - nameOrig: Originator ID
  - amount: Transaction amount
  - oldbalanceOrg, newbalanceOrig: Balances before and after
  - isFraud: Binary label indicating fraud

## Tech Stack
| Category | Tools |
|----------|-------|
| Languages | Python, PySpark |
| Cloud | AWS EMR, S3, Athena |
| Storage | Parquet |
| Machine Learning | Spark MLlib (Logistic Regression) |
| Visualization | Matplotlib, Athena queries |
| Other | Jupyter Notebook, AWS Console |

## Project Pipeline

### 1. Data Ingestion
- Raw CSV files were uploaded to Amazon S3
- Ingested into Spark DataFrames using `spark.read.csv()` with schema inference

### 2. Data Cleaning
- Removed duplicates using `dropDuplicates()`
- Filtered out rows with null values in key fields like `amount`

### 3. Feature Engineering
- Created derived features:
  - transaction_frequency per user
  - balance_diff = oldbalanceOrg - newbalanceOrig
  - Aggregate stats: average, total, and std dev of transactions per user

### 4. Data Storage
- Saved cleaned and transformed data as Parquet in S3
- Queried using AWS Athena

### 5. Model Training
- Assembled features with `VectorAssembler`
- Trained a Logistic Regression model on a 70/30 train-test split
- Evaluated using:
  - ROC-AUC (~0.99)
  - Precision / Recall / F1 Score
  - Confusion Matrix

## Visualizations & Insights

- Confusion Matrix: Shows high accuracy and true fraud detection
- ROC Curve: AUC score ~0.99, indicating strong classifier performance
- Feature Coefficients: transaction_frequency had the largest impact
- Athena Queries:
  - Top originators by total amount
  - Count of fraud vs non-fraud per user

## Architecture

### Current State:
- Batch processing using PySpark on EMR
- Querying with Athena

### Future State:
- Integrate AWS Kinesis for streaming
- Real-time model scoring via microservices

## Challenges & Benefits

### Challenges
- Imbalanced classes (fraud is rare)
- Memory limitations for large-scale datasets

### Distributed Benefits
- Scalable processing via Spark
- Efficient querying with Athena + Parquet
- Cloud-native deployment with minimal overhead

## Future Enhancements
- Add real-time fraud alerting with AWS Kinesis or Kafka
- Explore ensemble methods (Random Forest, XGBoost) or Deep Learning
- Incorporate user behavior or location-based features for higher precision

## About Me
This project was developed as part of my Master's in Data Science at DePaul University, where I specialized in Computational Methods. It reflects my experience with cloud-native data solutions and my passion for using ML to solve real-world challenges.

## Contact
- Name: Avinash Betha
- Email: avinashbetha35@gmail.com
- LinkedIn: [betha-avinash](https://linkedin.com/in/betha-avinash)
- GitHub: [avinash-betha](https://github.com/avinash-betha)
