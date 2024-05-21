# В этом разделе мы будем устанавливать и настраивать `Preometheus`
## Для начала нам нужно будем создать пользователя `prometheus` без домашний директории
~~~
sudo useradd --no-create-home --shell /bin/false prometheus
~~~
## Далее нам надо будет создать директорию для хранение конфигурационных файлов `/etc/prometheus`
~~~
sudo mkdir /etc/prometheus
~~~
## Так же нам надо будет создать директорию для того что бы хранить библиотеку `/var/lib/prometheus`
~~~
sudo mkdir /var/lib/prometheus
~~~
## Передаем прова нашему пользователю и группе до библиотеке  `/var/lib/prometheus`
~~~
sudo chown prometheus:prometheus /var/lib/prometheus
~~~
## C официального сайта нам надо будет скачать файлы `https://prometheus.io/download/`
## На момент данной инструкции `LTS` версия `2.45.5` качаем архим в директорию `tmp`
~~~
wget https://github.com/prometheus/prometheus/releases/download/v2.45.5/prometheus-2.45.5.linux-amd64.tar.gz -P /tmp/
~~~
## Далее нам надо разархивировать наш архив и `-C /tmp` данная команда разархивирет в директории `/tmp/`
~~~
tar -xvf /tmp/<file-name.tar.gz> -C /tmp/
~~~
