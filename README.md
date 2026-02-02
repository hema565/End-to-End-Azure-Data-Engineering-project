# End-to-End-Azure-Data-Engineering-project
## Payments & Orders Analytics platform 
### Problem This Project Solves
Fintech and e-commerce systems generate data from multiple sources (databases, APIs, event streams), but teams struggle with:

Reliable incremental ingestion
Duplicate, inconsistent, and low-quality data
Lack of analytics-ready models
Slow and unreliable business reporting

This project solves these challenges by building a production-grade Azure Lakehouse that delivers clean, trusted, and business-ready data for analytics.

### Solution Overview
An end-to-end data platform using the Bronze–Silver–Gold architecture that:

Ingests batch + streaming data
Applies data quality, deduplication, and schema enforcement
Models data using a star schema
Powers real-time and historical BI dashboards

## Architecture
![Architecture](Architecture/Architecture Diagram.png)
🏗️ Architecture Highlights

Sources: OLTP SQL DB (Users, Orders, Payments), REST APIs, Event Hub

Ingestion:

Azure Data Factory for CDC & incremental loads

Structured Streaming for real-time events

Storage: ADLS Gen2 + Delta Lake

Processing: Databricks (PySpark & SQL)

## Techstack used 
Azure Data Factory – Orchestration & ingestion

Azure Event Hub – Streaming ingestion

Azure Data Lake Gen2 – Storage

Delta Lake – ACID tables & versioning

Databricks (PySpark + SQL) – Transformations

Power BI – Visualization & analytics

## Dataset used

This project uses synthetically generated and real-time simulated data to replicate a production-like fintech environment.

1️⃣ OLTP Transactional Data (SQL Database)

Data Generation:
Transactional data for Users, Orders, and Payments was generated using the Python Faker library with Pandas.

Purpose:
To simulate realistic customer behavior, order volume, payment statuses, gateways, regions, and timestamps.

Storage:
The generated data was inserted into an Azure SQL Database, acting as the OLTP source system.

Ingestion:
Azure Data Factory pulls data incrementally from the SQL database using CDC / watermark-based ingestion into the Lakehouse Bronze layer.

👉 [View Dataset Folder](Datasets/oltp_transactional)

2️⃣ Currency Exchange Data (REST API)

Source:
Currency exchange rates are fetched from the Frankfurter public exchange rate API.

Usage:
Exchange rates are used to normalize multi-currency payment amounts into a base currency for analytics.

Ingestion Method:
Azure Data Factory performs date-based incremental API ingestion, storing raw responses in the Bronze layer before refinement in Silver.

👉 [View Dataset Folder](currency_exchange_rate)

3️⃣ Real-Time Events (Azure Event Hub)

Event Generation:
A custom Python producer simulates real-time payment and transaction events.

Streaming Platform:
Events are pushed to Azure Event Hub to mimic live payment processing systems.

Consumption:
Databricks Structured Streaming reads events from Event Hub and ingests them into the Bronze layer for near real-time processing

👉 [View Dataset Folder](eventhub)

## Data model

![Data model ER diagram](Entity_Relationship_Diagram.png)

## Kpi results at the end of notebook  
👉 [View fact_orders](https://hema565.github.io/End-to-End-Azure-Data-Engineering-project/Databricks/Gold/fact_orders.html)
👉 [View fact_payments](https://hema565.github.io/End-to-End-Azure-Data-Engineering-project/Databricks/Gold/fact_payments.html)
