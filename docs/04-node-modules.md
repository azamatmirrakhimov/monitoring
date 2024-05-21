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
##
~~~
systemctl daemon-reload
~~~
##
~~~
systemctl enable node_exporter.service
~~~
##
~~~
start node_exporter.service
~~~
##
~~~
status node_exporter.service
~~~

