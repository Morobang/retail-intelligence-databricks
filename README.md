# 🛒 Retail Intelligence Platform — Databricks End-to-End Project

![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=for-the-badge&logo=databricks&logoColor=white)
![Apache Spark](https://img.shields.io/badge/Apache_Spark-E25A1C?style=for-the-badge&logo=apachespark&logoColor=white)
![Delta Lake](https://img.shields.io/badge/Delta_Lake-00ADD8?style=for-the-badge&logo=delta&logoColor=white)
![MLflow](https://img.shields.io/badge/MLflow-0194E2?style=for-the-badge&logo=mlflow&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)

---

## 📌 Project Overview

This project is a full end-to-end **Retail Intelligence Platform** built entirely on **Databricks**, covering Data Engineering, SQL Analytics, and Machine Learning/AI in a single unified workspace.

The platform is modelled on the types of data problems that real e-commerce companies face daily — from understanding customer behaviour to predicting what to stock next month. The architecture follows the **Medallion Architecture (Bronze → Silver → Gold)** pattern used by leading data teams in production environments.

---

## ❓ The Problem Being Solved

E-commerce and retail companies generate millions of rows of transactional data every day but often struggle to turn that data into actionable decisions. Three critical business problems are addressed:

**1. Customer Churn** — Which customers are at risk of never buying again? Losing a customer costs 5–7x more than retaining one. The platform predicts churn probability per customer so retention teams can act proactively.

**2. Demand Forecasting** — How much stock is needed next month, per category, per region? Poor inventory management costs the global retail industry $1.75 trillion annually. The platform forecasts demand 30/60/90 days ahead.

**3. Revenue Intelligence** — Where is the business actually making money? Which product categories, sellers, and regions are driving growth vs dragging it down? Surfaced through a real-time SQL dashboard.

---

## 📦 Dataset

**Source:** [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) — Kaggle

| File | Description |
|---|---|
| `olist_orders_dataset.csv` | Core orders table — 100k orders from 2016–2018 |
| `olist_customers_dataset.csv` | Customer IDs and location |
| `olist_order_items_dataset.csv` | Line items purchased per order |
| `olist_order_payments_dataset.csv` | Payment method and installment data |
| `olist_order_reviews_dataset.csv` | Customer satisfaction scores and review text |
| `olist_products_dataset.csv` | Product categories, dimensions, and weights |
| `olist_sellers_dataset.csv` | Seller IDs and location |
| `olist_geolocation_dataset.csv` | Zip code latitude/longitude mapping |
| `product_category_name_translation.csv` | Portuguese → English category names |

> ⚠️ Raw data files are not stored in this repo. Download from Kaggle and upload to DBFS at `/FileStore/tables/olist/`

---

## 🏗️ Architecture
```
DATA SOURCES  →  BRONZE (Auto Loader + Delta Lake)
              →  SILVER (DLT + Data Quality Checks)
              →  GOLD   (Databricks SQL + KPIs)
              →  ML/AI  (MLflow + Spark ML + Feature Store)
              →  SERVING (Model Endpoints + Dashboards + Workflows)
```

Full Medallion Architecture — mirrors how production data teams build at scale.

---

## 🧰 Databricks Tools Used

| Tool | Purpose |
|---|---|
| Auto Loader | Incremental CSV ingestion into Bronze Delta tables |
| Delta Lake | ACID-compliant storage across all layers |
| Delta Live Tables | Declarative pipelines with data quality expectations |
| Unity Catalog | Governance, access control, and data lineage |
| Databricks SQL | Gold layer aggregations and business KPI queries |
| MLflow | Experiment tracking, model registry, versioning |
| Spark ML / XGBoost | Churn classification and demand forecasting |
| Feature Store | Reusable ML features shared across models |
| Model Serving | REST API for real-time churn predictions |
| Databricks Workflows | Full pipeline orchestration and scheduling |
| SQL Dashboards | Business intelligence and visualisation |

---

## 📁 Repository Structure
```
retail-intelligence-databricks/
├── README.md
├── data/
│   └── .gitkeep
├── notebooks/
│   ├── 01_bronze_ingestion/
│   │   └── autoloader_ingestion.py
│   ├── 02_silver_transformation/
│   │   └── silver_cleaning.py
│   ├── 03_gold_analytics/
│   │   └── gold_rfm_cohorts.py
│   └── 04_ml_models/
│       ├── churn_classifier.py
│       └── demand_forecast.py
├── pipelines/
│   └── dlt_pipeline.py
├── sql/
│   └── gold_queries.sql
├── workflows/
│   └── job_config.json
└── docs/
    └── architecture.png
```

---

## 🚀 Project Phases

**Phase 1 — Bronze:** Ingest all 9 Olist CSVs via Auto Loader into raw Delta tables. No transformations — exact source copy.

**Phase 2 — Silver:** Clean nulls, fix types, join all 9 tables, apply DLT data quality expectations.

**Phase 3 — Gold:** Build `gold_revenue_summary`, `gold_customer_cohorts`, `gold_rfm_scores`, `gold_inventory_signals` using Databricks SQL.

**Phase 4 — ML/AI:** Train Churn Classifier (XGBoost) and Demand Forecasting model. Track all experiments in MLflow.

**Phase 5 — Serving:** Deploy churn model as REST endpoint, build SQL Dashboard, schedule everything with Workflows.

---

## 📊 Business Questions Answered

- Which customers are most likely to churn in the next 30 days?
- What is predicted demand per product category for next quarter?
- Which categories and regions generate the most revenue?
- How do review scores correlate with repeat purchase rates?
- Which sellers have the best and worst delivery performance?
- What is the monthly cohort retention rate?

---

## 🛠️ Setup

1. Sign up at `community.cloud.databricks.com`
2. Download Olist dataset from Kaggle
3. Link this GitHub repo to Databricks via Repos
4. Upload CSVs to DBFS at `/FileStore/tables/olist/`
5. Create cluster with **Runtime 13.3 LTS ML**
6. Run notebooks sequentially starting from `01_bronze_ingestion`

---

## 👤 Author

Built as a portfolio project demonstrating end-to-end Databricks capabilities across Data Engineering, SQL Analytics, and ML/AI.

---

## 📄 License

MIT License. Olist dataset licensed under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).