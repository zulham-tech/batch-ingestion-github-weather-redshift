# Batch Ingestion Pipeline — GitHub + Weather APIs → Redshift

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Amazon Redshift](https://img.shields.io/badge/Amazon%20Redshift-8C4FFF?style=flat&logo=amazonredshift&logoColor=white)
![Apache Airflow](https://img.shields.io/badge/Apache%20Airflow-017CEE?style=flat&logo=apacheairflow&logoColor=white)
![AWS S3](https://img.shields.io/badge/AWS%20S3-FF9900?style=flat&logo=amazons3&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)

Automated batch ingestion pipeline that extracts data from GitHub REST API and OpenWeatherMap API, stages to S3, and loads into Amazon Redshift using the COPY command. Orchestrated by Apache Airflow with daily scheduling and incremental loads.

## Architecture

```mermaid
graph TD
    A[GitHub REST API<br/>Repos / Issues / PRs] --> C[Python Extractor<br/>Rate-limit aware]
    B[OpenWeatherMap API<br/>Historical Weather] --> C
    C --> D[AWS S3<br/>Raw Zone / Parquet]
    D --> E[Amazon Redshift<br/>COPY Command]
    E --> F[dbt Models<br/>Transformations]
    F --> G[Redshift Analytics<br/>BI Queries]
    H[Apache Airflow<br/>DAG Orchestration] --> C
    H --> E
    H --> F
```

## Features

- Paginated extraction from GitHub API with rate-limit handling
- Parallel weather data collection across multiple locations
- S3 staging with Parquet format for efficient COPY loads
- Incremental ingestion with watermark-based deduplication
- dbt transformation layer on top of Redshift
- Airflow DAGs with retry logic and Slack alerting on failure

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Extraction | Python (requests, aiohttp) |
| Staging | AWS S3 (Parquet) |
| Load | Amazon Redshift COPY |
| Transform | dbt Core |
| Orchestration | Apache Airflow 2.x |
| Infrastructure | Docker Compose |

## Prerequisites

- Docker & Docker Compose
- AWS credentials (S3 + Redshift access)
- GitHub Personal Access Token
- OpenWeatherMap API Key

## Quick Start

```bash
git clone https://github.com/zulham-tech/batch-ingestion-github-weather-redshift.git
cd batch-ingestion-github-weather-redshift
cp .env.example .env  # fill in API keys and AWS credentials
docker compose up -d
# Access Airflow at http://localhost:8080
```

## Project Structure

```
.
├── dags/                # Airflow DAG definitions
├── extractors/          # GitHub & Weather API clients
├── loaders/             # S3 uploader & Redshift COPY
├── dbt/                 # dbt models & tests
├── schemas/             # Redshift DDL scripts
├── docker-compose.yml
└── requirements.txt
```

## Author

**Ahmad Zulham** — [LinkedIn](https://linkedin.com/in/ahmad-zulham-665170279) | [GitHub](https://github.com/zulham-tech)
