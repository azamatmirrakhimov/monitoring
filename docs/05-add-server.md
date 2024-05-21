# Подключение серверов 
## Подключение серверов мы будем настраивать с начала на самом сервере далее на сервере мониторинга
## 1. Подключаемся к серверу который будем мониторить 
## Создадим директорию `node`
~~~
mkdir node
~~~
~~~
cd node
~~~
~~~
mkdir prometheus_db
~~~
~~~
vi docker-compose-node.yml
~~~
~~~
version: '3'
services:
  prometheus:
    image: prom/prometheus:latest
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
      - ./prometheus_db:/var/lib/prometheus
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
    ports:
      - '9090:9090'

  node-exporter:
    image: prom/node-exporter
    ports:
      - '9100:9100'

  cadvisor:
    image: gcr.io/cadvisor/cadvisor:latest
    ports:
      - '8081:8080'
    volumes:
      - /:/rootfs:ro
      - /var/run:/var/run:ro
      - /sys:/sys:ro
      - /var/lib/docker/:/var/lib/docker:ro
      - /dev/disk:/dev/disk:ro
    privileged: true
    devices:
      - /dev/kmsg
~~~
~~~
vi prometheus.yml
~~~
~~~
global:
   scrape_interval: 5s
   external_labels:
     monitor: 'jump-server'
 scrape_configs:
   - job_name: 'prometheus'
     static_configs:
       - targets: ['local_private_ip:9090']
   - job_name: 'node-exporter'
     static_configs:
       - targets: ['local_private_ip:9100']
   - job_name: 'cAdvisor'
     static_configs:
       - targets: ['local_private_ip:8081']
~~~
~~~
docker-compose -f docker-compose-node.yml up -d
~~~
