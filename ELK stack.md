# Introduction to ELK Stack

### contents :

- [What is ELK](#what-is-elk)
- [Elasticsearch](#elasticsearch)
- [Logstash and Kibana](#logstash-and-kibana)
- [Filebeat](#filebeat)

## What is ELK

ELK stands for Elastic search, Logstash and kibana. Elasticsearch is a search and analytics engine. Logstash is a server‑side data processing pipeline that ingests data from multiple sources simultaneously, transforms it, and then sends it to a "stash" like Elasticsearch. Kibana visualize that data and let’s user to understand and analyze them easily.

## Elasticsearch

The open source, distributed, RESTful, JSON-based search engine. Easy to use, scalable and flexible. It is NO_SQL database doc-oriented and high performance in plain text search.
It has indexing and sharding ability. And respond in a JSON format .

## Logstash and Kibana

users started using Elasticsearch for logs and wanted to easily ingest and visualize them. Enter Logstash, the powerful ingest pipeline, and Kibana, the flexible visualization tool.
Logstash includes 3 steps : input, filter and process data, output. And support plugins to work with other databases.
And kibana, is a GUI that help to understanding data easier with dashboard, charts and data tables. Kibana also can help to manage some parts of Elasticsearch.

## Filebeat

Filebeat is designed to read files from your system. It is particularly useful for system and application log files, but can be used for any text files that you would like to index to Elasticsearch in some way. In the logging case, it helps centralize logs and files in an efficient manner by reading from your various servers and VMs, then shipping to a central Logstash or Elasticsearch instance. Additionally, Filebeat eases the configuration process by including “modules” for grabbing common log file formats from MySQL, Apache, NGINX and more. These modules reduce the Filebeat configuration to a single command.

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
