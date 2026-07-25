# 🌍 Earthquake Data Pipeline

End-to-end Data Engineering project: collecting earthquake data from USGS API, storing it in MinIO (S3), loading into PostgreSQL and building analytical layer with Airflow + Metabase.

## 📌 Project Overview

The pipeline implements a classic medallion architecture:

**Raw → ODS → Analytical (Facts)**

| Layer | Description | Storage |
|-------|-------------|---------|
| **Raw** | Data from USGS Earthquake API | MinIO (Parquet) |
| **ODS** | Cleaned and structured data | PostgreSQL |
| **Analytical** | Daily aggregations (count & average magnitude) | PostgreSQL |

## 🏗 Architecture
USGS API
│
▼
┌─────────────────────┐
│  raw_from_api_to_s3 │  ← Airflow DAG
└─────────┬───────────┘
│
▼
MinIO (S3)
│
▼
┌─────────────────────┐
│  raw_from_s3_to_pg  │  ← Airflow DAG
└─────────┬───────────┘
│
▼
PostgreSQL (ODS)
│
├──────────────────────┐
▼                      ▼
┌──────────────────┐   ┌──────────────────────┐
│ fct_count_day... │   │ fct_avg_day_earthquake│
└──────────────────┘   └──────────────────────┘
│                      │
└──────────┬───────────┘
▼
Metabase
text## 🛠 Tech Stack

- **Orchestration**: Apache Airflow 2.10 (CeleryExecutor)
- **Object Storage**: MinIO (S3-compatible)
- **Databases**: PostgreSQL 13
- **Processing**: DuckDB
- **Visualization**: Metabase
- **Infrastructure**: Docker Compose

## 🚀 How to Run

### Prerequisites
- Docker & Docker Compose
- At least 4GB RAM recommended

### 1. Clone the repository
```bash
git clone https://github.com/evgeneverit/de_earthquake.git
cd de_earthquake
2. Create .env file
envAIRFLOW_UID=50000
AIRFLOW_PROJ_DIR=.
AIRFLOW_IMAGE_NAME=apache/airflow:2.10.5
_PIP_ADDITIONAL_REQUIREMENTS=duckdb
3. Start services
Bashdocker compose up -d
4. Access services

























ServiceURLCredentialsAirflowhttp://localhost:8080airflow / airflowMetabasehttp://localhost:3000-MinIO Consolehttp://localhost:9001minioadmin / minioadmin
📂 Project Structure
textde_earthquake/
├── dags/
│   ├── row_from_api_to_s3.py      # USGS API → MinIO
│   ├── raw_from_s3_to_pg.py       # MinIO → PostgreSQL
│   ├── fct_count_day_eqrthquake.py
│   └── fct_avg_day_earthquake.py
├── metabase/
│   └── Dockerfile
├── docker-compose.yaml
└── README.md
📊 DAGs Description






























DAGScheduleDescriptionraw_from_api_to_s3Daily 05:00Downloads earthquake data from USGS and saves as Parquet to MinIOraw_from_s3_to_pgDailyLoads raw data from MinIO into PostgreSQL ODS layerfct_count_day_earthquakeDailyCalculates daily earthquake countfct_avg_day_earthquakeDailyCalculates daily average magnitude
📈 Results
After successful runs you can explore:

Raw Parquet files in MinIO (prod/raw/earthquake/)
Cleaned data in PostgreSQL
Analytical tables with daily metrics
Dashboards in Metabase

👤 Author
Evgeny
GitHub: evgeneverit
