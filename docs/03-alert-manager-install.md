# В данном разделе мы будем устанавливать и настраивать `Alert Manager`
## Содаем пользователя `alertmanager` без доманний директории 
~~~
sudo useradd --no-create-home --shell /bin/false alertmanager
~~~
## Создаем раздел для хранение системных файлов
~~~
mkdit /etc/alermanager
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

~~~
