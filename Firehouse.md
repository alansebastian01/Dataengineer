**Amazon Kinesis Data Firehose** (now officially called **Amazon Data Firehose**) is a fully managed service that automatically captures, transforms, and delivers streaming data to storage and analytics destinations. Unlike Kinesis Data Streams, you don't manage shards or write consumer applications.

### How Firehose Works

```text
Data Producers
(Applications, IoT, CloudWatch, Kinesis Data Streams, MSK)

                │
                ▼
        Amazon Data Firehose
        - Buffers data
        - Optional Lambda transformation
        - Optional format conversion
        - Compression & encryption

                │
      ┌─────────┼──────────┐
      ▼         ▼          ▼
    Amazon S3  Redshift  OpenSearch
                │
              (via S3)
```

### Key Features

* **Fully managed**: No servers or shards to manage.
* **Automatic scaling**: Adjusts to incoming traffic.
* **Buffering**: Collects data based on size or time before delivering it.
* **Data transformation**: Can invoke an AWS Lambda function to modify records before delivery.
* **Compression**: Supports GZIP, Snappy, ZIP, and other formats.
* **Encryption**: Supports encryption in transit and at rest.
* **Format conversion**: Can convert JSON to Parquet or ORC for efficient analytics in S3.

### Supported Destinations

* Amazon S3
* Amazon Redshift
* Amazon OpenSearch Service
* Splunk
* Datadog
* New Relic
* HTTP endpoints
* Snowflake
* Apache Iceberg tables (supported in recent AWS updates)

### Firehose vs. Data Streams

| Feature            | Data Firehose                     | Kinesis Data Streams                   |
| ------------------ | --------------------------------- | -------------------------------------- |
| Real-time latency  | Seconds to minutes (buffered)     | Milliseconds                           |
| Shard management   | None                              | Required                               |
| Data retention     | No long-term retention            | 24 hours to 365 days                   |
| Multiple consumers | No                                | Yes                                    |
| Replay data        | No                                | Yes                                    |
| Processing         | Optional Lambda transformation    | Custom consumers, Lambda, KCL          |
| Best use case      | Deliver data to storage/analytics | Build real-time streaming applications |

### When to Use Firehose

Choose Firehose when you need to:

* Stream application or log data into Amazon S3 for data lakes.
* Load streaming data into Redshift for analytics.
* Index logs into OpenSearch.
* Send monitoring data to Splunk or Datadog.
* Avoid managing streaming infrastructure.

### Example

Suppose a website generates clickstream events:

1. The web application sends click events to Firehose.
2. Firehose buffers the data for, say, 60 seconds or until it reaches a size threshold.
3. A Lambda function enriches each event with additional metadata.
4. Firehose compresses the data and stores it in S3 as Parquet files.
5. Amazon Athena or Amazon Redshift queries the data for analytics.

### Interview Tip

A common interview question is:

> **Why would you choose Firehose over Kinesis Data Streams?**

A strong answer is:

> "Use Firehose when your primary goal is to reliably deliver streaming data to destinations like S3, Redshift, or OpenSearch with minimal operational overhead. Use Kinesis Data Streams when you need low-latency processing, multiple independent consumers, custom stream processing, or the ability to replay retained data."

In many AWS architectures, the two services are used together: producers write to **Kinesis Data Streams** for real-time processing, and **Amazon Data Firehose** reads from the stream to archive the data in S3 or load it into analytics systems.
