#  Node Exporter
## Данный модуль будет собирать данные с `linux` машин
## Создаем пользователя без домашний директории 
~~~
useradd --no-create-home --shell /bin/false node_exporter
~~~
## Скачиваем с официального сайта `https://prometheus.io/download/#node_exporter`
~~~
wget https://github.com/prometheus/node_exporter/releases/download/v1.8.0/node_exporter-1.8.0.linux-amd64.tar.gz -P /tmp/
~~~
## Далее разархивируем данные 
~~~
tar -xvf /tmp/<file_name>.tar.gz -C /tmp/
~~~
## Переходим в директорию 
~~~
cd /tmp/node_exporter-1.8.0.linux-amd64
~~~
## Смотрим что есть в данной директории 
~~~
ls -ll
~~~
Output
~~~
LICENSE
node_exporter
NOTICE
~~~
## Переносим файл в папку `/usr/local/bin/`
~~~
mv node_exporter /usr/local/bin/
~~~
## Передаем прова пользователю `node_exporter`
~~~
chown node_exporter:node_exporter /usr/local/bin/node_exporter 
~~~
## Теперь нам надо создать сервисный файл 
~~~
vi /etc/systemd/system/node_exporter.service
~~~
~~~
[Unit]
Description=Node_Exporter
After=network.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target
~~~
## Внесем коректировки в наш файл  
~~~
# my global config
global:
  scrape_interval: 15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
  evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
  # scrape_timeout is set to the global default (10s).

# Alertmanager configuration
alerting:
  alertmanagers:
    - static_configs:
        - targets:
           - localhost:9093

# Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
rule_files:
  # - "first_rules.yml"
  # - "second_rules.yml"

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: "prometheus"

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.

    static_configs:  
      - targets: ["localhost:9090"]
  - job_name: 'grafana' ## Создаем имя сервиса
    static_configs:     ## Статический конфиг
      - targets: ["localhost:3000"]  ## сервис и порт на которым он работает
  - job_name: 'alermanager'  ## Создаем имя сервиса
    static_configs:  ## Статический конфиг
      - targets: ["localhost:9093"] ## сервис и порт на которым он работает
  - job_name: 'node_exporter'  ## Создаем имя сервиса
    static_configs:  ## Статический конфиг
      - targets: ["localhost:9100"]  ## сервис и порт на которым он работает
~~~
## Перезапускаем `` для того что бы изменение в !! прменились
~~~
systemctl daemon-reload
~~~
## Добавим в автозапуск сервис
~~~
systemctl enable node_exporter.service
~~~
## Стартуем сервис
~~~
systemctl start node_exporter.service
~~~
## Проверяем статус 
~~~
systemctl status node_exporter.service
~~~

