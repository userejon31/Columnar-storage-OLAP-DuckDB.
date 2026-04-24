# Docker PostgreSQL Setup

This project uses a local PostgreSQL container for the benchmark comparison.

## Start PostgreSQL

```bash
docker compose up -d postgres
```

## Connection settings

- Host: `localhost`
- Port: `5432`
- Database: `postgres`
- User: `postgres`
- Password: `postgres`

## Stop PostgreSQL

```bash
docker compose down
```

The notebook uses the same connection string and can load the cleaned data into PostgreSQL once the container is running.
