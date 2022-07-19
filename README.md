# Elastic Stack (ELK), Grafana, Prometheus and Zipkin on Docker

This repository showcases an example docker setup for the [Seeker Swift Package](https://github.com/snkirov/seeker).

If you need a working example of the package, which can upload data to this docker setup see [Seeker Swift Examples](https://github.com/snkirov/seeker-swift-examples).

## Description

Run a fully functional observability server using the ELK-Stack, Grafana, Prometheus and Zipkin on Docker. 

It handles the collection and visualization of observability data - logs, metrics and traces.

ELK portion inspired by [devianthony](https://github.com/deviantony/docker-elk).

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

To access the Grafana web UI open http://localhost:5601 in a web browser and use the following (default) credentials to log in:

- user: admin
- password: admin

Upon the initial log in, Grafana will prompt you to change the password.

## Visualizing the data

The data visualization is done in Kibana for the logs and Grafana for metrics and traces. Here are some example visualizations in both [Grafana](https://grafana.com/docs/grafana/latest/dashboards/) and [Kibana](https://www.elastic.co/guide/en/kibana/current/dashboard.html). For further information please refer to the official documentation.

### Kibana

Access the Kibana web UI, navigate to `Analytics/Discover` and follow the instructions to setup your first log visualization.

Image placeholder
<br>

### Grafana

After logging in, the data sources need to be added. In the menu on the left navigate to `Configuration (Wheel Icon)/ Data Sources`. From there you should be able to add the data sources, in our case those would be Zipkin and Prometheus. Here's what Grafana should look like after adding the sources:

Image placeholder
<br>

And here is an example dashboard:

Image placeholder
<br>

## Contributing

Contributions to this project are welcome.

## License

This project is licensed under the MIT License. See [License](https://github.com/snkirov/seeker-docker-example/blob/master/LICENSE) for more information.
