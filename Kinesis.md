**Amazon Kinesis** is a fully managed AWS service for collecting, processing, and analyzing real-time streaming data.

It is commonly used for:

* Processing application logs
* IoT sensor data
* Clickstream analytics
* Real-time monitoring and alerting
* Financial transaction processing
* Video and audio streaming

### Main Kinesis Services

| Service                        | Purpose                                                                                                                                      |
| ------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------- |
| **Kinesis Data Streams (KDS)** | Capture and process real-time data streams with low latency.                                                                                 |
| **Kinesis Data Firehose**      | Deliver streaming data automatically to destinations like Amazon S3, Redshift, OpenSearch, or Splunk. No infrastructure management required. |
| **Kinesis Data Analytics**     | Analyze streaming data in real time using SQL or Apache Flink.                                                                               |
| **Kinesis Video Streams**      | Securely stream, store, and process video from cameras and devices.                                                                          |

### Architecture Example

```text
Applications / IoT Devices / Servers
             │
             ▼
     Kinesis Data Streams
             │
      ┌──────┴──────┐
      ▼             ▼
 Lambda        Consumer Apps
      │
      ▼
 Amazon S3 / DynamoDB / Redshift
```

### Key Concepts

* **Stream**: A sequence of continuously arriving data records.
* **Shard**: A unit of throughput in a Kinesis Data Stream.

  * Write capacity: **1 MB/sec or 1,000 records/sec**
  * Read capacity: **2 MB/sec**
* **Producer**: Sends data to Kinesis.
* **Consumer**: Reads and processes data from Kinesis.
* **Retention Period**: Data can be retained from **24 hours up to 365 days**.

### Advantages

* Fully managed and scalable
* Near real-time processing
* Integrates with AWS services like Lambda, S3, Redshift, DynamoDB, and OpenSearch
* Supports multiple consumers reading the same stream
* High durability and availability

### Common Use Cases

* Real-time dashboards
* Fraud detection
* Log aggregation
* IoT telemetry processing
* Live analytics
* Event-driven architectures

### Kinesis vs Apache Kafka

| Feature         | Kinesis                  | Kafka                                                  |
| --------------- | ------------------------ | ------------------------------------------------------ |
| Management      | Fully managed by AWS     | Self-managed or managed (MSK/Confluent)                |
| Scalability     | Automatic or shard-based | Partition-based                                        |
| AWS Integration | Excellent                | Good                                                   |
| Infrastructure  | No server management     | Requires cluster management unless using managed Kafka |
| Best For        | AWS-native applications  | Multi-cloud and large distributed event platforms      |

If you're preparing for an AWS interview, I can also explain **Kinesis Data Streams**, **Firehose**, **shards**, **partition keys**, **enhanced fan-out**, and **consumer types** with interview questions and practical examples.
