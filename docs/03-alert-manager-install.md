# В данном разделе мы будем устанавливать и настраивать `Alert Manager`
## Содаем пользователя `alertmanager` без доманний директории 
~~~
sudo useradd --no-create-home --shell /bin/false alertmanager
~~~
## Создаем раздел для хранение системных файлов
~~~
mkdir /etc/alertmanager
~~~
## Скачиваем файлы с официального сайта `https://prometheus.io/download/#alertmanager`
~~~
wget https://github.com/prometheus/alertmanager/releases/download/v0.27.0/alertmanager-0.27.0.linux-amd64.tar.gz -P /tmp/
~~~
## Далее нам надо разархивировать файл 
~~~
tar -xvf <file_name>.tar.gz -C /tmp/
~~~
## Переходим в директорию с разахивированым файлом
~~~
cd /tmp/alertmanager
~~~
## И переносим файлы по папкам 
~~~
sudo mv alertmanager /usr/local/bin/  
~~~
~~~
sudo mv amtool /usr/local/bin/
~~~
## Даем разришение пользователю 
~~~
sudo chown alertmanager:alertmanager /usr/local/bin/alertmanager
~~~
~~~
sudo chown alertmanager:alertmanager /usr/local/bin/amtool
~~~
## Переносим кофигурационный файл
~~~
sudo mv alertmanager.yml /etc/alertmanager
~~~
## Даем прова пользователю 
~~~
sudo chown -R alertmanager:alertmanager /etc/alertmanager/
~~~
## Создаем сервисный файл 
~~~
sudo vim /etc/systemd/system/alertmanager.service
~~~
~~~
[Unit]
Description=Alertmanager
Wants=network-online.target
After=network-online.target

[Service]
User=alertmanager
Group=alertmanager
Type=simple
WorkingDirectory=/etc/alertmanager/
ExecStart=/usr/local/bin/alertmanager \
    --config.file=/etc/alertmanager/alertmanager.yml

[Install]
WantedBy=multi-user.target
~~~
## Далее в файле с настройками `prometheus.yml` нужно изменить настройки для `alertmanager`
~~~
sudo vim /etc/prometheus/prometheus.yml
~~~
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
          # - alertmanager:9093   <-- Разкоментировать данный раздел "alertmanager" заменить на "localhost"

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
~~~
