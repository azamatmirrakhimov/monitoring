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


