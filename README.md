Big Data Project Using Docker Containers
This project demonstrates a hands-on implementation of Big Data technologies like Hadoop, Spark, Hive, Kafka, and more using Docker. The goal is to create a distributed environment where each service runs in its own container, providing a scalable and flexible setup similar to a production environment.


System Requirements
Docker must be installed on your machine.
Allocate at least 4 GB of RAM to Docker for this project to run smoothly. 
The project has been developed and tested using Python and PySpark.
Technology Stack
Technology	Version
Hadoop	2.7.4
Spark	2.4.1
Kafka	2.12-2.2.1
Hive	2.3.2
ZooKeeper	3.4.10
Jupyter	Latest
Business Model
This project simulates a real-world e-commerce business process:

A user data is sent  to a Kafka topic (users).
The event data from Kafka is processed using Spark Streaming.
The processed data is then stored in Hadoop HDFS using Hive SQL queries for reporting and analysis.
Jupyter Notebooks can be used for querying and displaying insights from the stored data.
How to Run the Project
1. Start All Services
Start all the required services (Hadoop, Kafka, Spark, Hive, etc.) using the Docker Compose file provided in the project directory. Run the following command in your terminal:

bash
Copy code
docker-compose up -d
This will start all the services in detached mode. It may take a few minutes for all the services to start up.

2. Run Kafka Producer (Simulate Checkout Process)
To simulate the customer checkout process and send product order data to a Kafka topic named users, run the following command:


docker exec -it kafka /opt/kafka/bin/kafka-console-producer.sh \
  --broker-list localhost:9092 --topic users
You can input JSON messages representing product orders directly in the terminal.

Example message:

json
Copy code
{"id": "1", "first_name": "John", "last_name": "Doe", "email": "john.doe@example.com", "age": 25, "gender": "male", "state": "CA", "created_at": "2025-01-01"}
3. Deploy and Run Spark Streaming Job
Deploy the Spark Streaming Job to consume data from the Kafka topic and save it to Hadoop HDFS using Hive SQL.

Run the following command to submit your PySpark job:


docker exec -it spark-master /opt/spark/bin/spark-submit \
  /opt/spark-apps/spark_kafka_hive.py
The Spark job will:

Read real-time data from the Kafka topic: users.
Parse the incoming JSON data.
Write batch data to Hadoop HDFS by executing Hive SQL queries.
Directory Structure
Copy code
BDA_PROJECT/
├── hadoop/
├── kafka/
├── spark/
├── hive/
├── jupyter/
├── docker-compose.yml
└── spark_kafka_hive.py
Accessing Services
Service	URL
Hadoop Namenode	http://localhost:50070
Spark Master	http://localhost:8080
Hive Metastore	thrift://localhost:9083
Jupyter Notebook	http://localhost:8888
Conclusion
This project provides a complete Big Data ecosystem running on Docker. It replicates a production-like environment, where each service can be maintained and upgraded independently. 
