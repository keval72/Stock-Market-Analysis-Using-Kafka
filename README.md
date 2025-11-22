# Stock Market Real-Time Data Analysis Using Apache Kafka

## Overview
This project demonstrates real-time data analysis of stock market data using Apache Kafka. The pipeline involves streaming data, processing it, and storing it in AWS services for querying and analysis. The project showcases the core components of Kafka and AWS integration.

---

## Architecture

<img width="797" alt="Screenshot 2025-11-22" src="https://github.com/keval72/Stock-Market-Analysis-Using-Kafka/blob/main/img/Stock%20Market%20Project.png" />

---



## Introduction to Apache Kafka
Apache Kafka is a distributed event store and stream-processing platform. It is designed for high-throughput and fault-tolerant real-time data pipelines.

### Core Kafka Architecture
1. **Producer**: Sends messages to Kafka topics.
2. **Kafka Brokers**: Kafka brokers store messages and manage multiple partitions within topics. Brokers are nodes in a Kafka cluster.
3. **Consumers**: Retrieve messages from topics for processing.
4. **ZooKeeper**: Manages the Kafka cluster, including failure detection, recovery, and maintaining configuration information.

#### ZooKeeper Responsibilities:
- Cluster management.
- Failure detection and recovery.
- Storing access control lists and secrets.
- Distributed synchronization.
- Maintaining configuration information.

---

## Key Kafka Concepts
### Topics
Topics act as logical buckets within Kafka brokers and represent streams of related messages. Developers define topics based on use cases, and Kafka allows for unlimited topics.

- **Partitions**: Each topic can have multiple partitions, which act as logs for messages. Partitions are replicated across brokers for fault tolerance.
- **Replication**: Replicas ensure that data is available even if a broker fails.

### Message Flow
1. **Producer**: Writes data (messages) to topics.
2. **Broker**: Stores and manages messages across partitions.
3. **Consumer**: Pulls data from topics for processing. Kafka consumers automatically retrieve new messages from assigned partitions.

---

## Implementation Steps

### 1. Setting Up an AWS EC2 Instance
- **Create an EC2 instance** and download its key pair.
- Copy the SSH command to connect to the instance from your local machine.

#### Connect and Setup:
1. Install Java and Kafka on the EC2 instance.
2. Start ZooKeeper and Kafka servers:
    - Use separate terminals for ZooKeeper and Kafka servers.
    - Update Kafka server configuration to use the instance's public IP for external access.
3. Configure AWS security:
    - Modify the security group's inbound rules to allow all traffic (Anywhere-IPv4).
4. Open two more terminal for producer and consumer.


Basically, there must be 4 terminals (zookeeper, kafka server, Prodcuer, Consumer).

All terminals must be connected to the ec2 instance and must be inside the kafka directory.


Run the commands from `command.txt` to ensure the correct setup.

### 2. Simulating Stock Market Data
Since real-time stock market data is not accessible, simulated data is generated using Python.

#### Implementation:
1. Create two Jupyter notebooks:
    - **Producer.ipynb**: Sends simulated data to Kafka topics as a stream.
    - **Consumer.ipynb**: Reads and processes data from Kafka topics.
2. Verify data flow in both Jupyter notebooks and terminal outputs.


### 3. Storing Data in AWS S3
- **Create an S3 bucket** for storing processed data.

#### Configure AWS CLI:
1. Set up AWS IAM:
    - Add a new user with administrative access.
    - Download the Access Key ID and Secret Key.
2. Install and configure AWS CLI on your local machine:
    ```bash
    aws configure
    ```
3. Stream data from the local machine to the S3 bucket as JSON files.

### 4. Data Transformation and Querying with AWS Glue and Athena

#### AWS Glue Setup:
1. **Crawler**:
    - Create a new crawler in AWS Glue.
    - Add S3 as the data source.
    - Configure IAM roles to allow Glue access to S3.
2. **Database**:
    - Create a new database in Glue.
    - Run the crawler to create tables from JSON files in S3.

#### Querying Data with Athena:
1. Open Athena and select the created database.
2. Configure Athena output location in a new S3 bucket.
3. Query the data stored in S3 tables.

---

## Technical Justification
1. **Why Kafka?**
   - Kafka's distributed architecture ensures high throughput and fault tolerance, making it ideal for real-time streaming applications like stock market data analysis.
2. **Role of Partitions:**
   - Partitions enable parallel processing of data, enhancing performance and scalability.
3. **AWS S3 Integration:**
   - S3 offers a cost-effective and scalable storage solution for data pipelines.
4. **AWS Glue & Athena:**
   - Glue simplifies ETL processes, while Athena allows for serverless SQL querying, making data analysis efficient.

---

## Results
- Simulated stock market data is successfully streamed, processed, and stored.
- Data is queried and analyzed using AWS Glue and Athena, demonstrating end-to-end pipeline functionality.

---

This project demonstrates a scalable and efficient architecture for real-time data processing, leveraging the strengths of Kafka and AWS cloud services.
