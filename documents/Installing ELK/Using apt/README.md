#  Installing ELK using package manager

- [Introduction](#introduction)
- [Installing ElK, using package managers](#installing-elk-using-package-managers)

## Introduction

ELK Stack, also known as the Elastic Stack, is a powerful open-source tool used for log management and data analysis. It consists of three main components: Elasticsearch, Logstash, and Kibana.

Elasticsearch is a distributed search and analytics engine that helps to store and index large volumes of data. Logstash is a data processing pipeline that collects, filters, and transforms logs and other data sources. Kibana is a visualization tool that enables users to explore and visualize data through interactive dashboards and charts.

## Installing ElK, using package managers

I reference you to this link below, but i'll give you a summery in 4 steps.
<https://vegastack.com/tutorials/how-to-install-elk-stack-on-ubuntu-20-04/>

### Step 1 - Install and Configure the Elasticsearch

Use CURL, the command-line tool for transferring data with URLs.

```bash
curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
```

Add the Elastic source list to the `sources.list.d` directory. It is where APT will search for the new sources:

```bash
echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list
```

Update the package lists. It will enable APT to read the new Elastic source:

```bash
sudo apt update
```

 Install the Elasticsearch with the below command:

 ```bash
sudo apt install elasticsearch 
```

 Use your preferrence for a text editor. It will let you edit Elasticsearch’s main configuration file, `elasticsearch.yml`

```bash
sudo nano /etc/elasticsearch/elasticsearch.yml
```

The Elasticsearch listens for traffic from everywhere on the port `9200`.
To restrict access and increase security, find the line mentioning network.host then, uncomment it, and replace its value with `localhost` like:

```bash
etc/elasticsearch/elasticsearch.yml
. . .
# ------------------------------ Network -------------------------------
#
# Set the bind address to a specific IP (IPv4 or IPv6):
#
network.host: localhost
. . .
```

 If you want to listen only on a specific interface, specify the IP instead of `localhost`. Now, save and then close `elasticsearch.yml`.

 Start the Elasticsearch service with the `systemctl`. Give Elasticsearch little time to start up

 ```bash
sudo systemctl start elasticsearch
```

 Run the below command. It will enable Elasticsearch to start every time your server boots:

 ```bash
sudo systemctl enable elasticsearch
```

You can check the status of Elasticsearch to sure about your service is running

 ```bash
sudo systemctl status elasticsearch
```

You will then test whether your Elasticsearch service is running. Do it by sending an HTTP request:

 ```bash
curl -X GET "localhost:9200"
```

 After that,you can see a response indicating some basic information. It is basically about your local node, similar to:

  ```bash
Output
{
  "name" : "Elasticsearch",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "qqhFHPigQ9e2lk-a7AvLNQ",
  "version" : {
    "number" : "7.7.1",
    "build_flavor" : "default",
    "build_type" : "deb",
    "build_hash" : "ef48eb35cf30adf4db14086e8aabd07ef6fb113f",
    "build_date" : "2020-03-26T06:34:37.794943Z",
    "build_snapshot" : false,
    "lucene_version" : "8.5.1",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
```

### Step 2 - Installing and Configuring the Logstash

You will install Logstash with follow command:

 ```bash
sudo apt install logstash
```

Then enable and start the logstash service using the below command:

 ```bash
sudo systemctl enable logstash
sudo systemctl start logstash
sudo systemctl status logstash
```

You can also see and change the logstash configuration file :

 ```bash
sodu nano /etc/logstas/logstash.yml
```

### Step 3 - Installing and Configuring Kibana Dashboard

You can install kibana using this command

 ```bash
sudo apt install kibana
```

Then enable and start the Kibana service using the below command:

 ```bash
sudo systemctl enable kibana
sudo systemctl start kibana
sudo systemctl status kibana
```

You can also see and change the logstash configuration file :

```bash
sudo nano /etc/kibana/kibana.yml
```

uncomment this below lines:

```bash
> server.port: 5601
> server.host: "localhost"
> elasticsearch.hosts: ["http://localhost:9200"]
```

and also replace `"localhost"` with `"0.0.0.0"` (means any api address)

After changing configuration file you need to restart kibana

```bash
sudo systemctl restart kibana
```

To access kibana, open a web browser and browse to the `http://ip_address:5601` address

### Step 4 - Installing and configuration Filebeat

Let's install Filebeat:

```bash
sudo apt install filebeat
```

open configuration file using below command:

```bash
sudo nano /etc/filebeat/filebeat.yml
```

in Elasticsearch output section, comment out the flowing lines:

```bash
output.elasticsearch:
   Array of hosts to connect to.
   hosts: ["localhost:9200"]
```

in Logstash output section, uncomment the flowing lines:

```bash
output.logstash:
  # The Logstash hosts
  hosts: ["localhost:5044"]
```

Enable the filebeat system module :

```bash
sudo filebeat modules enable system
```

You will see a list of enabled and disabled modules by running:

```bash
sudo filebeat modules list
```

By default, configuration of Filebeat is complete to use default paths for the syslog and authorization logs. Here, you will not change anything in the configuration. You will see the parameters of the module in `/etc/filebeat/modules.d/system.yml` configuration file.

Next, load the index template into Elasticsearch. The Elasticsearch index is a collection of documents having similar features. Indexes are identified with a name. It is useful to refer to the index when performing various operations within it. The index template gets applied automatically when creating a new index.
You will now load the template, with the following command:

```bash
sudo filebeat setup --index-management -E output.logstash.enabled=false -E 'output.elasticsearch.hosts=["0.0.0.0:9200"]'
```

> "0.0.0.0" means any ip address

Filebeat comes with sample Kibana dashboard that allows you to visualize the Filebeat data in Kibana. Before you use dashboards, you need to create the index pattern. Then, load the dashboards into Kibana. As dashboards load, Filebeat connects to Elasticsearch checking the version information. So, to load dashboards when enabling the Logstash, disable the Logstash output, then enable Elasticsearch output:

```bash
sudo filebeat setup -E output.logstash.enabled=false -E output.elasticsearch.hosts=['0.0.0.0:9200'] -E setup.kibana.host=localhost:5601
```

Now we should start and enable the filebeat service:

```bash
sudo systemctl start filebeat
sudo systemctl enable filebeat
sudo systemctl status filebeat
```

If the Elastic Stack set-up is correct. The Filebeat will begin shipping your syslog and authorization logs to Logstash. It will then load that data into the Elasticsearch.
Then, to verify that Elasticsearch is indeed receiving this data, you will have to query the Filebeat index with the following command:

```bash
curl -XGET 'http://localhost:9200/filebeat-*/_search?pretty'
```
