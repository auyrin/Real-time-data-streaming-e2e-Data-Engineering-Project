# Realtime Data Streaming | End-to-End Data Engineering Project

## Overview:
This project is a real-time data streaming and processing pipeline designed to handle high-velocity data streams, perform real-time analytics, 
and store processed data for further querying and analysis. The system leverages modern big data technologies such as Apache Kafka, Apache Spark, 
Apache Cassandra, and Apache Airflow, all containerized and orchestrated using Docker. This ensures a robust, scalable, and efficient data 
processing architecture that is easy to deploy, manage, and scale.

## Key Components:
1. #### Apache Kafka:
- Acts as the data ingestion layer, collecting and storing real-time data streams (e.g., user events, logs, or sensor data).
- Topics (e.g., users_created) are used to organize and partition data streams.
  
2. #### Apache Spark:
- Serves as the streaming data processing engine, consuming data from Kafka topics in real-time.
- Performs transformations, aggregations, and analytics on the streaming data.
- Writes processed data to a sink (e.g., Cassandra) for persistent storage.

3. #### Apache Cassandra:
- Acts as the data storage layer, storing processed data for querying and further analysis.
- Provides high availability, scalability, and fault tolerance for large-scale data.

4. #### Apache Airflow:
- Orchestrates and schedules data processing workflows, including Spark jobs.
- Ensures that data pipelines run reliably and efficiently.

5. #### ZooKeeper:
- Manages and coordinates Kafka brokers, ensuring high availability and fault tolerance.

6.  #### Docker:
- Provides a containerized environment for deploying and managing all components (Kafka, Spark, Cassandra, Airflow, Zookeeper).
- Ensures consistency, scalability, and ease of maintenance across development, testing, and production environments.

## System Workflow:
#### Data Ingestion:
- Real-time data is ingested into Kafka topics (e.g., users_created).

#### Data Processing:
- Spark Streaming consumes data from Kafka topics, processes it (e.g., filtering, aggregation, enrichment), and writes the results to Cassandra.

#### Data Storage:
- Processed data is stored in Cassandra for persistent storage and querying.

#### Orchestration:
- Airflow schedules and monitors Spark jobs, ensuring that data pipelines run as expected.

#### Containerization:
- All components (Kafka, Spark, Cassandra, Airflow, Zookeeper) are containerized using Docker, ensuring portability, scalability, and ease of deployment.

## Key Features:
- Real-Time Processing: Enables real-time analytics and insights on streaming data.
- Scalability: Designed to handle large volumes of data with distributed processing and storage.
- Fault Tolerance: Ensures high availability and reliability through Kafka, Spark, and Cassandra.
- Orchestration: Automates and monitors data pipelines using Airflow.
- Containerization: Uses Docker to ensure consistency, portability, and ease of deployment.

## Use Cases:
1. #### Real-Time User Analytics:
- Process user events (e.g., clicks, purchases) in real-time to generate insights and metrics.

2. #### IoT Data Processing:
- Handle high-velocity sensor data streams and perform real-time anomaly detection.

3. #### Log Processing:
- Ingest and analyze log data in real-time for monitoring and troubleshooting.
