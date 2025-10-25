# MLOps-end-to-end-advanced
Built MLOps pipeline end-to-end from data ingestion, cleaning, feature engineering, Optuna, training, Hyperparameter tuning, validating, selecting best model, model validation, promotion and inference.

# 🚀 Advanced MLOps Project: Customer Churn Prediction (v1.0)

This repository contains the end-to-end implementation of an advanced Machine Learning Operations (MLOps) project for customer churn prediction, leveraging Databricks, MLflow, and Unity Catalog for governance, automation, and real-time serving.

The pipeline covers feature engineering, automated hyperparameter tuning, CI/CD setup, real-time model serving, and continuous production monitoring.

## 🛠️ Technology Stack

* **Platform:** Databricks Lakehouse Platform
* **Data/Governance:** Delta Lake, Unity Catalog (UC)
* **Feature Management:** Databricks Feature Store, Online Tables
* **ML Tracking & Registry:** MLflow (Experiments & Unity Catalog Model Registry)
* **Hyperparameter Tuning:** Optuna
* **Serving:** Databricks Model Serving (REST API)
* **Monitoring:** Databricks Model Monitoring, Drift Detection

## 💡 Project Workflow Breakdown

| Step | Notebook | Key Work & Contribution |
| :--- | :--- | :--- |
| **1. Feature Engineering & Store** | `01_data_cleaning.python` | Transformed raw data and created the **`advanced_churn_feature_table`** in the **Databricks Feature Store** (governed by UC). This establishes a single source of truth for features, using `customerID` and `transaction_ts` as primary/timeseries keys for better data governance. |
| **2. Advanced Model Training** | `02_model_training_with_optuna.python` | Implemented advanced **Hyperparameter Tuning** using the **Optuna** framework. All runs and the optimal hyperparameters were automatically tracked and logged to **MLflow Experiments** for reproducibility. |
| **3. Model Registration & CI/CD Setup** | `03b_from_notebook_to_models_in_uc.python`, `03a_create_model_deployment_job.python` | Registered the best model from the Optuna runs into the **Unity Catalog Model Registry** (`sai_datastorage.default.advanced_mlops_churn`). Also created a deployment job (`DBDemos-Model-Deployment-Job`) for seamless CI/CD integration. |
| **4. Challenger Validation Gate** | `04a_challenger_validation.python` | Implemented a rigorous **Validation Gate**. The model is evaluated not just on F1 score, but against custom **Business Metrics** (cost/revenue impact) to decide if the new Challenger can replace the Champion model. |
| **5. Model Promotion & Approval** | `04b_challenger_approval.python` | Final automated logic to check for a specific approval tag (`Approval_Check`) and promote the validated Challenger to the **`@Champion`** alias in UC, making it live for all downstream consumers. |
| **6. Production Inference (Batch & Real-Time)** | `05_batch_inference.python`, `06_serve_features_and_model.python` | Deployed for multiple use cases: **Batch Scoring** using a Spark UDF (`05_batch_inference.python`) and **Real-Time Serving** by deploying features to **Online Tables** and the model to a **Model Serving REST API endpoint** (`06_serve_features_and_model.python`). |
| **7. Continuous Monitoring & Drift** | `07_model_monitoring.python`, `08_drift_detection.python` | [cite_start]Established **Model Monitoring** in production to track performance metrics and **Drift Detection** against baseline data to catch feature degradation before it impacts business outcomes. [cite: 9, 10] |
