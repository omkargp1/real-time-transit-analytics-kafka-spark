# 🚍 Real-Time Bus Boarding Data Analysis

### Apache Kafka + Apache Spark Structured Streaming + MLlib

Author: **Omkar Pardeshi**\
Course: DATA603 -- Platforms for Big Data Processing\
Date: May 2025

------------------------------------------------------------------------

## 📌 Project Overview

This project implements a **real-time public transportation analytics
system** using:

-   **Apache Kafka** → Data Streaming\
-   **Apache Spark Structured Streaming** → Real-time Processing\
-   **Spark MLlib** → Predictive & Anomaly Detection

The system processes live boarding data to:

-   Detect bus bunching\
-   Predict passenger demand\
-   Identify anomalies\
-   Track top 10 busiest bus stops\
-   Detect low-activity / delayed stops

------------------------------------------------------------------------

## 🏗️ System Architecture

    CSV File
       ↓
    Kafka Producer (Python)
       ↓
    Kafka Topic: boarding-data
       ↓
    Spark Structured Streaming
       ↓
    Analytics + ML Models
       ↓
    Console / Parquet / Memory Table

------------------------------------------------------------------------

## 📂 Project Structure

    ├── boarding_data_producer.ipynb
    ├── boarding_data_live_data_analysis.ipynb
    ├── models/
    ├── docker-compose.yml
    └── README.md

------------------------------------------------------------------------

## 🧩 Implementation Details

### 1️⃣ Kafka Producer

Streams CSV data row-by-row into Kafka topic `boarding-data`.

``` python
for _, row in df.iterrows():
    record = row.to_dict()
    producer.send(topic, value=record)
    producer.flush()
    time.sleep(0.1)
```

------------------------------------------------------------------------

### 2️⃣ Spark Structured Streaming Consumer

Subscribes to Kafka topic and parses JSON messages using a defined
schema.

``` python
stream_df = spark.readStream   .format("kafka")   .option("kafka.bootstrap.servers", "ed-kafka:29092")   .option("subscribe", "boarding-data")   .load()
```

------------------------------------------------------------------------

### 3️⃣ Bus Bunching Detection

Detects buses arriving within a 2-minute window at the same stop.

------------------------------------------------------------------------

### 4️⃣ Passenger Count Prediction

Uses Spark MLlib `LinearRegression()` to predict boarding demand.

------------------------------------------------------------------------

### 5️⃣ Anomaly Detection

Uses Z-score method:

    z = (x - mean) / std_dev

Flags anomalies where:

    z_score > 3

------------------------------------------------------------------------

### 6️⃣ Top 10 Busiest Bus Stops

Uses streaming aggregation and memory sink for real-time querying.

------------------------------------------------------------------------

## ⚙️ How to Run

### 1. Start Docker

    docker-compose up -d

### 2. Run Kafka Producer Notebook

    boarding_data_producer.ipynb

### 3. Run Spark Streaming Notebook

    boarding_data_live_data_analysis.ipynb

### 4. Monitor Services

-   Jupyter → localhost:8888\
-   Spark UI → localhost:4040\
-   Kafka → localhost:9092

------------------------------------------------------------------------

## 🚀 Achievements

✅ End-to-end real-time streaming pipeline\
✅ Integrated ML model training in micro-batches\
✅ Window-based streaming analytics\
✅ Scalable architecture

------------------------------------------------------------------------

## 🔮 Future Work

-   Deploy on Kubernetes\
-   Add Grafana dashboards\
-   Implement deep learning forecasting\
-   Add alerting system

------------------------------------------------------------------------

## 📚 References

-   Apache Spark Documentation\
-   Apache Kafka Documentation\
-   Spark MLlib Guide
