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
