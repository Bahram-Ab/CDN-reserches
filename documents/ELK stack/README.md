# Introduction to ELK Stack

### contents :

- [Introduction to ELK Stack](#introduction-to-elk-stack)
    - [contents :](#contents-)
  - [What is ELK](#what-is-elk)
  - [Elasticsearch](#elasticsearch)
  - [Logstash and Kibana](#logstash-and-kibana)
  - [Filebeat](#filebeat)
  - [PS. difference between SQL and No-SQL](#ps-difference-between-sql-and-no-sql)

## What is ELK

ELK stands for Elasticsearch, Logstash, and Kibana. Elasticsearch is a search and analytics engine. Logstash is a server‑side data processing pipeline that ingests data[^data-ingesting] from multiple sources simultaneously, transforms it, and then sends it to a "stash" like Elasticsearch. Kibana visualizes that data and let user understand and analyze them easily.

[^data-ingesting]: Data ingestion is the process of importing large, assorted data files from multiple sources into a single, cloud-based storage medium where it can be accessed and analyzed.

## Elasticsearch

The open-source, distributed, RESTful, JSON-based search engine, is scalable, and flexible. It is a No_SQL database Document-oriented[^Document-oriented]and high-performance in plain text search.
It has indexing[^Indexing] and sharding[^data-base-sharding] ability to boost performance and overcome store and process limitations.

[^Document-oriented]: They store data as documents, which can be JSON, BSON, or other formats. Each document represents a single entity or object and contains all of the relevant data for that entity.
[^Indexing]: Indexing is the process of creating data structures that allow for efficient data retrieval.
[^data-base-sharding]: Database sharding is the process of storing a large database across multiple machines.

## Logstash and Kibana

Users can use Elasticsearch for logs. Now they want to easy ingest and visualize them. So two important technologies were developed. Logstash, the ingest pipeline, and Kibana, the flexible visualization tool.
Logstash includes three steps: input data, filter and process them, and output the final result. It can support plugins to work with other databases.
Kibana is a GUI that helps to understand data easier with dashboards, charts, and data tables. Kibana also can help to manage some parts of Elasticsearch.

## Filebeat

Filebeat is designed to read files from your system. It is particularly useful for system and application log files. But can be used for any text files that you would like to index to Elasticsearch in some way. In the logging case, it helps efficiently centralize logs and files by reading from your various servers and VMs, then shipping them to a central Logstash or Elasticsearch instance. Additionally, Filebeat eases the configuration process by including “modules” for grabbing common log file formats from MySQL, Apache, NGINX, and more. These modules reduce the Filebeat configuration to a single command.

![ELK Stack modeling](ELKStackModel.webp)

## PS. difference between SQL and No-SQL

NoSQL (not only SQL) databases are non-tabular databases and store data differently than relational tables. NoSQL databases come in a variety of types based on their data model. The main types are document, key-value, wide-column, and graph. Here is a comparison between SQL and NoSQL:

| SQL                                                                                                | NoSQL                                                                     |
| -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| Relational database management system (RDBMS)                                                      | Non-relational database management system                                 |
| Suitable for structured data with predefined schema                                                | Suitable for unstructured and semi-structured data                        |
| Data is stored in tables with columns and rows                                                     | Data is stored in collections or documents                                |
| Follows ACID properties (Atomicity, Consistency, Isolation, Durability) for transaction management | follows CAP theorem (Consistency, Availability, and Partition tolerance). |
| Supports JOIN and complex queries                                                                  | Does not support JOIN and complex queries                                 |
| Uses normalized data structure                                                                     | Uses denormalized data structure                                          |
| Requires vertical scaling to handle large volumes of data                                          | Horizontal scaling is possible to handle large volumes of data            |
