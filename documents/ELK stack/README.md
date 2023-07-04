# Introduction to ELK Stack

### contents :

- [What is ELK](#what-is-elk)
- [Elasticsearch](#elasticsearch)
- [Logstash and Kibana](#logstash-and-kibana)
- [Filebeat](#filebeat)

Here's a sentence with a footnote. [^hello]

[^hello]: This is the footnote.

## What is ELK

ELK stands for Elasticsearch, Logstash, and Kibana. Elasticsearch is a search and analytics engine. Logstash is a server‑side data processing pipeline that ingests data from multiple sources simultaneously, transforms it, and then sends it to a "stash" like Elasticsearch. Kibana visualizes that data and let user understand and analyze them easily.

## Elasticsearch

The open source, distributed, RESTful, JSON-based search engine. Easy to use, scalable, and flexible. It is NO_SQL database doc-oriented and high performance in plain text search.
It has indexing and sharding ability. And respond in a JSON format.

## Logstash and Kibana

Users started using Elasticsearch for logs and wanted to easily ingest and visualize them. Enter Logstash, the ingest pipeline, and Kibana, the flexible visualization tool.
Logstash includes three steps: input, filter and process data, and output. And support plugins to work with other databases.
Kibana is a GUI that helps to understand data easier with dashboards, charts, and data tables. Kibana also can help to manage some parts of Elasticsearch.

## Filebeat

Filebeat is designed to read files from your system. It is particularly useful for system and application log files. but can be used for any text files that you would like to index to Elasticsearch in some way. In the logging case, it helps efficiently centralize logs and files by reading from your various servers and VMs, then shipping them to a central Logstash or Elasticsearch instance. Additionally, Filebeat eases the configuration process by including “modules” for grabbing common log file formats from MySQL, Apache, NGINX, and more. These modules reduce the Filebeat configuration to a single command.

![ELK Stack modeling](ELKStackModel.webp)

### ps. difference between sql and no-sql

| SQL                                                                                                | NoSQL                                                                     |
| -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| Relational database management system (RDBMS)                                                      | Non-relational database management system                                 |
| Suitable for structured data with predefined schema                                                | Suitable for unstructured and semi-structured data                        |
| Data is stored in tables with columns and rows                                                     | Data is stored in collections or documents                                |
| Follows ACID properties (Atomicity, Consistency, Isolation, Durability) for transaction management | follows CAP theorem (Consistency, Availability, and Partition tolerance). |
| Supports JOIN and complex queries                                                                  | Does not support JOIN and complex queries                                 |
| Uses normalized data structure                                                                     | Uses denormalized data structure                                          |
| Requires vertical scaling to handle large volumes of data                                          | Horizontal scaling is possible to handle large volumes of data            |

Data ingestion is the process of importing large, assorted data files from multiple sources into a single, cloud-based storage medium where it can be accessed and analyzed.
