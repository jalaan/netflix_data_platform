# End-to-End “Netflix-style” Data Platform

This project simulates a **production-grade analytics data platform** inspired by Netflix-scale architectures. It demonstrates how raw behavioral events can be transformed into analytics-ready datasets, monitored through orchestration, and consumed via dashboards — using modern data engineering and analytics engineering best practices.

The goal of this project is to showcase **end-to-end ownership** of a data platform: from ingestion and storage to transformation, testing, orchestration, and analytics delivery.

---

## What This Project Demonstrates

- End-to-end data platform design (ingestion → lake → warehouse → marts → dashboard)
- Analytics engineering using **dbt** (staging, marts, tests, documentation)
- Pipeline orchestration and observability using **Dagster**
- SQL-first analytics modeling with **DuckDB**
- Python-based ETL and synthetic event generation
- Data quality validation and pipeline health auditing
- Clear separation of raw, transformed, and business-facing data layers

---

## Tech Stack

- **Python** — event generation, ingestion, orchestration logic
- **DuckDB** — analytical warehouse
- **dbt** — transformations, tests, analytics models
- **Dagster** — pipeline orchestration and visualization
- **Streamlit** — analytics dashboard
- **Parquet** — data lake storage format

---

## Architecture Overview

### 1. Event Generation
Synthetic Netflix-style watch events are generated using Python.  
Events include users, titles, timestamps, and engagement metrics to simulate real-world streaming behavior.

### 2. Data Lake
Raw events are written to a partitioned Parquet-based data lake.  
Data is organized by `event_date` to support scalable analytics patterns.

### 3. Warehouse
Data is loaded into **DuckDB**, serving as a lightweight analytical warehouse.  
Raw tables are created for users, titles, and events.

### 4. Analytics Engineering (dbt)
Transformations are handled using dbt with a layered approach:
- **Staging models** clean and standardize raw data
- **Fact and dimension tables** model user behavior and content consumption
- **Marts** expose business-ready KPIs
- **Tests** ensure data validity and pipeline reliability

### 5. Orchestration & Monitoring
Dagster orchestrates the full pipeline, coordinating ingestion, loading, and transformations.  
Pipeline runs are audited and tracked to support observability and health monitoring.

### 6. Dashboard
A Streamlit dashboard provides visibility into key metrics, trends, and top-performing titles.

---

## Screenshots

### Streamlit Dashboard
![Dashboard](assets/screenshots/dashboard.png)

### dbt Build (Models + Tests)
![dbt build](assets/screenshots/dbt-build.png)

### Dagster Orchestration Graph
![Dagster](assets/screenshots/dagster-orchestration.png)

### Project Structure
![Structure](assets/screenshots/project-structure.png)

### Pipeline Health & Audit History
![Pipeline Health](assets/screenshots/pipeline-health.png)

---

## Key Data Models

- **stg_events / stg_users / stg_titles** — cleaned staging models
- **fct_watch** — fact table capturing watch behavior
- **dim_user / dim_title** — dimension tables
- **mart_daily_kpis** — daily engagement metrics
- **mart_top_titles** — top-performing content
- **audit_pipeline_runs** — pipeline execution history

---

## Why This Project Matters

This project mirrors how modern data teams operate at scale:

- SQL-first analytics modeling
- Strong separation of concerns between raw, transformed, and business data
- Automated testing and data quality checks
- Orchestration with visibility into pipeline execution
- Analytics delivered through consumable dashboards

It demonstrates the ability to **design, build, and reason about data platforms**, not just write isolated scripts.

---

## How to Run Locally (Optional)

```bash
# activate environment
source venv/bin/activate

# generate events
python src/generate_events.py

# ingest into data lake
python src/ingest_to_lake.py

# load into warehouse
python src/load_to_duckdb.py

# run dbt models
cd dbt/netflix_analytics
dbt build

# launch dashboard
streamlit run dashboard/app.py
