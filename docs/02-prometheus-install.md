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
## Далее нам надо перейти в директорию 
~~~
cd /tmp/
~~~
~~~
ls -ll
~~~
Output
~~~
total 229792
drwxr-xr-x 2 prometheus 127      4096 May  2 14:42 console_libraries
drwxr-xr-x 2 prometheus 127      4096 May  2 14:42 consoles
-rw-r--r-- 1 prometheus 127     11357 May  2 14:42 LICENSE
-rw-r--r-- 1 prometheus 127      3773 May  2 14:42 NOTICE
-rwxr-xr-x 1 prometheus 127 121066245 May  2 14:00 prometheus
-rw-r--r-- 1 prometheus 127       934 May  2 14:42 prometheus.yml
-rwxr-xr-x 1 prometheus 127 114206977 May  2 14:01 promtool
~~~
## Далее с помощю команды `mv` перенести файлы в нужные директории
~~~
sudo mv console* /etc/prometheus/
~~~


