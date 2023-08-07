# Installing ELK using Docker

- [Introduction](#introduction)
- [installation](#installation)

## Introduction

ELK Stack, also known as the Elastic Stack, is a powerful open-source tool used for log management and data analysis. It consists of three main components: Elasticsearch, Logstash, and Kibana.

Elasticsearch is a distributed search and analytics engine that helps to store and index large volumes of data. Logstash is a data processing pipeline that collects, filters, and transforms logs and other data sources. Kibana is a visualization tool that enables users to explore and visualize data through interactive dashboards and charts.

## Installation

We will use docker to install ELK, so for easy manage containers, we will use docker-compose. This is easy work, so let's do that in 4 steps. For cleaner structure you can wrap all your files, with a directory. I named it `elk`.

### Step 1 - Create docker-compose configuration

For using docker compose, you should configure `docker-compose.yml` file first. I placed it following of this doc for easy use.
Notice that you absolutely can change it for your need, specially your volume destinations.

Then you should change the image tags that placed in above of image tag for each container to a compatible version. you can check it by searching your image name and viewing the *tags* tab in [docker_hub](https://hub.docker.com/) website.

### Step 2 - Configuring the Logstash

You should also configure your logstash pipelines. I placed it following of this doc too. You should copy it to a directory named *logstash* beside the *docker-compose* file.

### Step 3 - Installing docker-compose

Docker-compose helps you to easily manage your images and containers. You can install it by using this command in your CLI :
```bash
  sudo apt install docker-compose
```

### Step 4 - getting your containers up

Finally you can build and start your containers using this command:

```bash 
  docker-compose up
```
> take a notice that you should be in your wrapper directory (that i call it **elk**) while running this command