# Batch Ingestion Pipeline | GitHub API & Weather Archive â†’ Redshift

> **Type:** Batch | **Stack:** GitHub API + Open-Meteo â†’ Kafka â†’ PySpark â†’ PostgreSQL â†’ S3 â†’ Redshift â†’ Airflow

## Key Metrics
- **<15 minutes** end-to-end SLA (daily 01:00â€“03:00 WIB)
- **~1,200 records/day** from 2 independent sources
- **Idempotent design:** batch_date partitioning prevents duplicates
- **Redshift optimized:** DISTKEY + SORTKEY + AZ64 compression

## Architecture
```
GitHub REST API          Open-Meteo Historical API
        â†“                           â†“
Kafka [batch-github-repos]   Kafka [batch-weather-history]
                â†“ (PySpark batch)
        PySpark Transform â†’ dedup â†’ feature engineering
                â†“
        PostgreSQL (staging) â†’ S3 (Parquet) â†’ Amazon Redshift
```

## Feature Engineering
| Feature | Formula |
|---|---|
| activity_score | starsÃ—0.5 + forksÃ—0.3 + watchersÃ—0.2 |
| stars_per_day | stars / repo_age_days |
| temp_range_c | temp_max - temp_min |
| is_rainy | precipitation_sum > 1mm |

## Tech Stack
Python Â· Apache Kafka Â· PySpark Â· Airflow Â· PostgreSQL Â· Amazon S3 (Parquet) Â· Amazon Redshift Â· Docker

## Author
**Ahmad Zulham Hamdan** | [LinkedIn](https://linkedin.com/in/ahmad-zulham-hamdan-665170279) | [GitHub](https://github.com/zulham-tech)
