# Implementation APM in ELK stack 

### contents :

- [Implementation APM in ELK stack](#implementation-apm-in-elk-stack)
    - [contents :](#contents-)
  - [What is APM](#what-is-apm)
  - [APM in Elastic stack](#apm-in-elastic-stack)
  - [Structure](#structure)
  - [That's Here I'm](#thats-here-im)

## What is APM

Application performance monitoring (APM) is the practice of tracking key software application performance metrics using monitoring software and telemetry data. Practitioners use APM to ensure system availability, optimize service performance and response times, and improve user experiences.

Mobile apps, websites, and business applications are typical use cases for monitoring. However, with today’s highly connected digital world, monitoring use cases expand to the services, processes, hosts, logs, networks, and end-users that access these applications — including a company’s customers and employees.
for more info you can see [this](https://www.dynatrace.com/news/blog/what-is-apm-2/) website.

## APM in Elastic stack

In Elastic stack you can have APM to monitor your application performance. Application can be any thing with any language. For quick start APM in Elastic cloud, you can visit [this](https://www.elastic.co/guide/en/apm/guide/current/apm-quick-start.html) link.

## Structure

To implement APM you need to collect data, send it to ELK stack, and explore and visualize it by kibana. For collecting data you should have an agent on your application. You can use [official documentation](https://www.elastic.co/guide/en/apm/guide/current/apm-quick-start.html#add-apm-integration-agents)  and use your specific application language section. And by [configuring the APM integration ](https://www.elastic.co/guide/en/apm/guide/current/apm-quick-start.html#add-apm-integration) 

I have an example for my flask application and using OpenSearch as my integration: 

1. Set up a virtual environment (optional but recommended): It's good practice to create a virtual environment to isolate your Flask project dependencies. Open a terminal or command prompt and navigate to your project directory. Then, run the following command to create a virtual environment:
```bash
    python -m venv <your-env-name>
```

2. Activate the virtual environment: Activate the virtual environment by running the appropriate command for your operating system:
```bash
    source <your-env-name>/bin/activate
```

3.  Install Flask: With the virtual environment activated, run the following command to install Flask:
```bash
    pip install flask
```

4.  Verify the installation: You can verify that Flask is installed correctly by running the following command:
```bash
    flask --version
```

5. Install the Elastic APM agent using pip: 
```bash
    pip install elastic-apm[flask]
```

6. Build your application (.py): 
```python
    from flask import Flask
    from elasticapm.contrib.flask import ElasticAPM
    from elasticapm.traces import capture_span


    app = Flask(__name__)
    app.config["ELASTIC_APM"] = {
        # Set required service name. Allowed characters:
        # a-z, A-Z, 0-9, -, _, and space
        "SERVICE_NAME": '<your-service-name>',
        # Use if APM Server requires a token
        "SECRET_TOKEN": '<your-secret-token>',
        # Set custom APM Server URL (default: http://localhost:8200)
        "SERVER_URL": '<your-apm-server-url>',
    }

    apm = ElasticAPM(app)


    # code to capture
    @app.route("/")
    def hello():
        with capture_span("hello", "custom") as span:
            span.set_label("custom_label", "custom_value")
            return "Hello, World!"


    if __name__ == "__main__":
        app.run()
```

7. Run Flask application:
```bash
    python <app-name>.py
```

8. you should configure and run the AOM server, I link you to my [Docker-compose](./docker-compose.yml) file to configure APM server, OpenSearch node and OpenSearch dashboard.

9.  Save the `docker-compose.yml` file and run the following command to start the APM Server alongside your OpenSearch cluster:
```bash 
    docker-compose up -d
```

10. Verify that the APM Server is running by accessing its status endpoint in your web browser:
```
    http://localhost:8200/
```


## That's Here I'm

But in the OpenSearch you can't easily explore the APM data in Elastic stack by installing plugin and configuring the Kibana dashboard.
For implementing APM in OpenSearch you should use `OpenTelemetry Collector`. Here i give you the answer of ChatGPT for asking **what is  OpenTelemetry Collector**: 

>    The OpenTelemetry Collector is a component of the OpenTelemetry project that collects, processes, and exports telemetry data from various sources, including applications, services, and infrastructure. It acts as a flexible and vendor-agnostic intermediary between the instrumentation (APM agents, SDKs, etc.) and the back-end monitoring systems.
>    Here's an overview of what the OpenTelemetry Collector does:
>1. Data Collection: The OpenTelemetry Collector collects telemetry data from various sources, such as APM agents, SDKs, log files, and metrics endpoints. It supports multiple protocols and formats, allowing it to gather data from different languages, frameworks, and systems.
>2. Data Processing: Once the data is collected, the OpenTelemetry Collector performs various processing tasks on the telemetry data. It can enrich, transform, and filter the data based on configuration rules. This processing may include adding contextual information, aggregating metrics, sampling, and more.
>3. Exporting: After processing, the OpenTelemetry Collector exports the telemetry data to one or more back-end monitoring systems. It supports a wide range of exporters, including popular monitoring platforms like OpenSearch, Elasticsearch, Prometheus, Jaeger, and more. This allows you to send the collected data to your preferred monitoring solution.
>4. Flexibility and Compatibility: The OpenTelemetry Collector is designed to be highly flexible and compatible with various monitoring systems and instrumentation libraries. It provides a unified way to collect and export telemetry data, regardless of the underlying technologies used in your applications and infrastructure.
>
>
>By using the OpenTelemetry Collector with OpenSearch, you can leverage its capabilities to collect and export APM data from your applications and services to OpenSearch for monitoring and analysis. It simplifies the integration process and allows you to use OpenSearch as part of your overall APM solution.
>
>It's important to note that the OpenTelemetry Collector is just one component of the OpenTelemetry project, which aims to provide a standardized approach to observability and telemetry across different systems and platforms. It consists of a set of APIs, SDKs, and other components that enable you to instrument your applications and collect telemetry data in a consistent and vendor-agnostic manner.

In the end I give you some link that may be useful for your continue: 

- [Trace analytics in OpenSearch](https://opensearch.org/docs/latest/data-prepper/common-use-cases/trace-analytics/)
- [Performance Analyzer in OpenSearch](https://opensearch.org/docs/latest/monitoring-your-cluster/pa/index/)
- [Managing OpenSearch Dashboards plugins](https://opensearch.org/docs/latest/install-and-configure/install-dashboards/plugins/)
- [A blog about building a distributed tracing pipeline with OpenTelemetry Collector, Data Prepper, and OpenSearch Trace Analytics](https://opensearch.org/blog/distributed-tracing-pipeline-with-opentelemetry/)
- [Official documentation of OpenTelemetry collector](https://opentelemetry.io/docs/collector/)

Good luck :)
