# 🏥 Clinical Trial Patient Recruitment and Adherence Monitoring Dashboard

## Executive Summary
This project implemented a **central command center** to monitor the performance of a multi-site clinical trial. The primary objective was to reduce the high costs and delays associated with poor patient recruitment and non-adherence by providing trial managers with **real-time, actionable insights**.

The solution integrates clinical trial data (screening, enrollment, visits) with a machine learning model to create a secure, interactive Business Intelligence (BI) dashboard.

## Key Deliverables & Insights
* **Recruitment Funnel Visualization:** Tracks patient flow from Screened (100 total) to Enrolled (17 total) to Randomized (62 total), showing an observed **Screen Failure Rate of 0.21**.
* **Dropout Risk Prediction:** A key feature is the integration of a Machine Learning model (Logistic Regression) to flag patients at high risk of dropout.
    * **Key Finding:** The dashboard indicated that **43.04%** of currently enrolled patients were flagged as high risk, necessitating immediate intervention.
* **Site Performance Leaderboard:** Ranks sites by **Enrollment Velocity** (e.g., SITE05 was the top performer) and compares **Average Medication Adherence** scores (e.g., SITE05 had the highest at 76.98%; SITE01 had the lowest at 56.52%)[cite: 61, 62, 63].
* **Patient Adherence:** Provides a Visit Status Breakdown, showing a positive 83.54% completed visits, but highlighting **12.03% Missed** and **4.43% Rescheduled** visits.
* **Security (RLS):** Implemented **Row-Level Security (RLS)** using `UserPatientMap.csv` to ensure site monitors only view data for the patients/sites they are responsible for.

## Technical Stack
* **Tool:** Power BI (Business Intelligence Dashboard)
* **Modeling:** Python / Jupyter Notebook / Google Colab (for ML Model Training)
* **Model Type:** Classification (Logistic Regression) to predict binary outcome: Dropout (1) or No Dropout (0) 
* **Security:** Row-Level Security (RLS) implementation

## Data Engineering & Modeling
* **Data Sources:** Five simulated extracts from the Electronic Data Capture (EDC) system were integrated, including `site_metadata.csv`, `screening.csv`, `enrollment.csv`, `visits.csv`, and `UserPatientMap.csv`.
* **Data Model:** A robust **Star Schema** was constructed, with the main visits data serving as the core **Fact Table**.
* **Feature Engineering:** Features critical for the dropout model were engineered, such as Calculating Missed Visit Count and Average Medication Adherence per patient.
* **Model Integration:** The trained model scored the current population, generating a `dropout_predictions.csv` file, which was then imported into the Power BI data model to power the "At-Risk" patient visual.

## Future Enhancements
1.  **Alert Automation:** Integrate the dropout risk score to automatically send SMS/email alerts to site coordinators when a patient's risk crosses a threshold.
2.  **Survival Analysis:** Implement an advanced model to estimate the **time-to-dropout** for better resource planning and intervention timing.
3.  **Explainability:** Incorporate feature-level explainability (e.g., SHAP values) into the dashboard to show *why* a patient was flagged (e.g., "due to 3 Missed Visits and Adherence below 60%").
