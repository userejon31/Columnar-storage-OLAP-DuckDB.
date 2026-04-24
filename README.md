# Columnar Storage, OLAP, DuckDB, and PostgreSQL Benchmark

This repository contains the final assignment work for comparing an OLAP-style engine (DuckDB) against an OLTP-style engine (PostgreSQL) using Airbnb data stored in Parquet files.

The project includes:

- an English report notebook with theory and practice,
- a data-cleaning pipeline from raw Parquet to strongly typed datasets,
- reproducible benchmark queries executed on both DuckDB and PostgreSQL,
- Docker-based PostgreSQL setup for local testing,
- generated benchmark artifacts (CSV and chart).

## Repository Contents

- `assignment_report.ipynb`: main report and executable workflow.
- `docker-compose.yml`: local PostgreSQL service definition.
- `docker-postgres-README.md`: quick Docker notes.
- `artifacts/listings_clean.parquet`: cleaned listings dataset.
- `artifacts/past_rates_clean.parquet`: cleaned rates dataset.
- `artifacts/benchmark_comparison.csv`: benchmark results table.
- `artifacts/benchmark_comparison.png`: benchmark chart.

## Prerequisites

- Python environment with notebook dependencies installed.
- Docker and Docker Compose.
- Source files available in the expected data directory:
	- `listings.parquet`
	- `past_rates.parquet`
	- `benchmark_queries.sql`

The notebook currently points to:

- `PROJECT_DIR = /home/jose/Documentos/Project Databases`
- `REPO_DIR = /home/jose/Documentos/GitHub/Columnar-storage-OLAP-DuckDB.`

If your local paths are different, update those constants in `assignment_report.ipynb` (Environment Setup section).

## Quick Start

1. Start PostgreSQL in Docker:

```bash
docker compose up -d postgres
```

2. Open and run `assignment_report.ipynb` from top to bottom.

3. Verify generated outputs in `artifacts/`.

4. Stop containers when done:

```bash
docker compose down
```

## Docker Runtime Conditions

The PostgreSQL container is configured as follows:

- image: `postgres:16`
- container name: `columnar-olap-postgres`
- host port: `5432`
- database: `postgres`
- user: `postgres`
- password: `postgres`
- restart policy: `unless-stopped`

Health check:

- command: `pg_isready -U postgres -d postgres`
- interval: `5s`
- timeout: `5s`
- retries: `10`

## Benchmark Notes

- Each query is run at least 3 times per engine.
- DuckDB reads directly from cleaned Parquet files.
- PostgreSQL loads cleaned data into typed tables before timing.
- The final chart uses a log-scale y-axis to handle large timing differences across query patterns.

## What to Submit

Required:

1. `assignment_report.ipynb`
2. `docker-compose.yml`
3. `docker-postgres-README.md`
4. `artifacts/listings_clean.parquet`
5. `artifacts/past_rates_clean.parquet`
6. `artifacts/benchmark_comparison.csv`
7. `artifacts/benchmark_comparison.png`

Also include the provided benchmark SQL file used in your run:

8. `benchmark_queries.sql` (from your assignment data directory)

Optional (if requested by your course):

- exported PDF version of the notebook report.