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
USGS API -> raw_from_api_to_s3 (Airflow DAG) -> MinIO (S3) -> raw_from_s3_to_pg (Airflow DAG) -> PostgreSQL (ODS) -> Metabase


- **Orchestration**: Apache Airflow 2.10 (CeleryExecutor)
- **Object Storage**: MinIO (S3-compatible)
- **Databases**: PostgreSQL 13
- **Processing**: DuckDB
- **Visualization**: Metabase
- **Infrastructure**: Docker Compose


👤 Author
Evgeny
GitHub: evgeneverit
