# Batch Ingestion Pipeline | GitHub API & Weather Archive -> Redshift

**Stack:** GitHub API + Open-Meteo Historical -> Kafka -> PySpark -> PostgreSQL -> S3 -> Redshift -> Airflow

## Key Metrics
- Less than 15 minutes end-to-end SLA (daily 01:00-03:00 WIB)
- ~1,200 records/day from 2 independent sources
- Idempotent design: batch_date partitioning prevents duplicates
- Redshift optimized: DISTKEY + SORTKEY + AZ64 compression

## Feature Engineering
| Feature | Formula |
|---|---|
| activity_score | stars x 0.5 + forks x 0.3 + watchers x 0.2 |
| stars_per_day | stars / repo_age_days |
| temp_range_c | temp_max - temp_min |
| is_rainy | precipitation_sum > 1mm |

## Tech Stack
Python, Apache Kafka, PySpark, Airflow, PostgreSQL, Amazon S3 Parquet, Amazon Redshift, Docker

## Author
Ahmad Zulham Hamdan | https://linkedin.com/in/ahmad-zulham-665170279
