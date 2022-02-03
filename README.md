# springboot-monitor Docker Stack with Prometheus + Grafana
a prometheus and grafana docker container to monitor springboot api

Stand-up a Docker [Prometheus](http://prometheus.io/) stack containing Prometheus, Grafana to collect and graph springboot reliability and throughput.

## Pre-requisites

Make sure Docker and [Docker Compose](https://docs.docker.com/compose/install/) are installed on your Docker host machine.

## Quick Start

```
git clone https://github.com/sucrewar/springbot-monitor
cd springbot-monitor
docker-compose up -d
```

Go to [http://localhost:3030/d/7voUGKrik/spring-cloud-gateway](http://http://localhost:3030/d/7voUGKrik/spring-cloud-gateway) (change `localhost` to your docker host ip/name).

## Configuration

To change what hosts you ping you change the `targets` section in [/prometheus/prometheus.yaml](./prometheus/prometheus.yaml) file.


Once configurations are done, run the following command:

    $ docker-compose up -d

That's it. docker-compose builds the entire Grafana and Prometheus stack automagically.

The Grafana Dashboard is now accessible via: `http://<Host IP Address>:3030` for example http://localhost:3030

username - admin
password - admin (Password is stored in the `config.monitoring` env file)

The DataSource and Dashboard for Grafana are automatically provisioned.

If all works it should be available at http://localhost:3030/d/7voUGKrik/spring-cloud-gateway - if no data shows up try change the timeduration to something smaller.

## Interesting urls

http://localhost:9090/targets shows status of monitored targets as seen from prometheus - in this case which hosts being pinged and speedtest. note: speedtest will take a while before it shows as UP as it takes about 30s to respond.

http://localhost:9090/graph?g0.expr=probe_http_status_code&g0.tab=1 shows prometheus value for `probe_http_status_code` for each host. You can edit/play with additional values. Useful to check everything is okey in prometheus (in case Grafana is not showing the data you expect).

## Thanks and a disclaimer
This setup is not secured in any way, so please only use on non-public networks, or find a way to secure it on your own.