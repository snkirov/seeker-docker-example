# Elastic Stack (ELK), Grafana, Prometheus and Zipkin on Docker

ELK portion created by [devianthony](https://github.com/deviantony/docker-elk).

Run a fully functional observability backend using the ELK-Stack, Grafana, Prometheus and Zipkin using Docker. 
<br>
<br>
It handles the collection and visualization of observability data - logs, metrics and traces.

## Usage 

By default, the stack exposes the following ports:

<h6> Logs </h6>
<ul>
  <li> 5044: Logstash Beats input </li>
  <li> 5000: Logstash TCP input </li>
  <li> 9600: Logstash monitoring API </li>
  <li> 9200: Elasticsearch HTTP </li>
  <li> 9300: Elasticsearch TCP transport </li>
  <li> 5601: Kibana </li>
</ul>

<h6> Metrics and Traces </h6>
<ul>
  <li> 9090: Prometheus </li>
  <li> 9091: Prometheus Pushgateway </li>
  <li> 9411: Zipkin </li>
  <li> 4317: Open Telemetry Collector </li>
  <li> 3000: Grafana </li>
</ul>

## Bringing up the stack

Clone this repository onto the Docker host that will run the stack, then start the stack's services locally using Docker Compose:

```
$ docker-compose up
```

You can also run all services in the background (detached mode) by appending the -d flag to the above command.

### Logs

Give Kibana about a minute to initialize, then access the Kibana web UI by opening http://localhost:5601 in a web browser and use the following (default) credentials to log in:

- user: elastic
- password: changeme

Upon the initial startup, the elastic, logstash_internal and kibana_system Elasticsearch users are intialized with the values of the passwords defined in the .env file ("changeme" by default). The first one is the built-in superuser, the other two are used by Kibana and Logstash respectively to communicate with Elasticsearch. This task is only performed during the initial startup of the stack. To change users' passwords after they have been initialized, please refer to the instructions by [devianthony](https://github.com/deviantony/docker-elk#initial-setup).

### Metrics and Traces
