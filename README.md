# Realtime Data Streaming | End-to-End Data Engineering Project

## Table of Contents
- [Introduction](#introduction)
- [System Architecture](#system-architecture)
- [Technologies](#technologies)
- [Getting Started](#getting-started)

## Introduction

This project serves as a comprehensive guide to building an end-to-end data engineering pipeline. It covers each stage from data ingestion to processing and finally to storage, utilizing a robust tech stack that includes Apache Airflow, Python, Apache Kafka, Apache Zookeeper, Apache Spark, and Cassandra. Everything is containerized using Docker for ease of deployment and scalability.

## System Architecture

![System Architecture](https://github.com/airscholar/e2e-data-engineering/blob/main/Data%20engineering%20architecture.png)

The project is designed with the following components:

- **Data Source**: We use `randomuser.me` API to generate random user data for our pipeline.
- **Apache Airflow**: Responsible for orchestrating the pipeline and storing fetched data in a PostgreSQL database.
- **Apache Kafka and Zookeeper**: Used for streaming data from PostgreSQL to the processing engine.
- **Control Center and Schema Registry**: Helps in monitoring and schema management of our Kafka streams.
- **Apache Spark**: For data processing with its master and worker nodes.
- **Cassandra**: Where the processed data will be stored.


## Technologies

- Apache Airflow
- Python
- Apache Kafka
- Apache Zookeeper
- Apache Spark
- Cassandra
- PostgreSQL
- Docker

## Getting Started

1. Clone the repository:
    ```bash
    git clone https://github.com/airscholar/e2e-data-engineering.git
    ```

2. Navigate to the project directory:
    ```bash
    cd e2e-data-engineering
    ```

3. Run Docker Compose to spin up the services:
    ```bash
    docker-compose up
    ```
4. Trigger the Airflow DAG:

    Option A: Trigger from Airflow UI

Open browser: http://localhost:8080
Log in (default: airflow / airflow)
Trigger your DAG manually

Option B: Trigger from CLI (inside Airflow container)

    ```bash
    docker exec -it <airflow-container-name> bash
airflow dags trigger <your_dag_id>
    ```

5.  Ensure Kafka Receives Data:
    ```bash
    docker exec -it <kafka-container-name> kafka-console-consumer \
  --bootstrap-server localhost:9092 \
  --topic <your_topic> \
  --from-beginning
    ```

6.  Run the Spark Application:
    ```bash
    docker exec -it <spark-container> /opt/spark/bin/spark-submit \
  --class <your_main_class> \
  --master local[*] \
  <your_jar_or_script_path>
    ```
7.  Query Cassandra for Inserted Records:
    ```bash
  docker exec -it <cassandra-container> cqlsh
    ```
