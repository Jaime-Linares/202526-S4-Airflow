# Airflow + PostgreSQL + Kafka Stack

This repository contains a minimal Docker setup with only:

- Airflow
- PostgreSQL (Airflow metadata database)
- Kafka in KRaft mode (no ZooKeeper)

## Services

- Airflow Web UI: `http://localhost:8081`
- PostgreSQL: `localhost:5432`
- Kafka (host): `localhost:9092`
- Kafka (internal Docker network): `kafka:29092`

## Start

```bash
docker compose up -d --build
```

## Stop

```bash
docker compose down
```

## Airflow credentials

- Username: `admin`
- Password: `admin`

## Available DAGs

DAGs are mounted from `src/dags_demo`.

Current demo DAGs:

- `dag_kafka.py`
- `dag_hello.py`
- `dag_random.py`

## Create a Kafka topic

From your host:

```bash
docker compose exec kafka kafka-topics --create --topic test_topic --partitions 1 --replication-factor 1 --bootstrap-server kafka:29092
```

List topics:

```bash
docker compose exec kafka kafka-topics --list --bootstrap-server kafka:29092
```

## Notes

- ZooKeeper is not used.
- Airflow creates a `kafka_default` connection on startup.
- If you need a clean reset:

```bash
docker compose down -v
```
