# How to install Alert manager
## 1. Step we need to create user
~~~
sudo useradd --no-create-home --shell /bin/false alertmanager
~~~
## 2. Create directory for file config
~~~
sudo mkdir /etc/alertmanager
~~~
## 3. Dowload Alermanager for oficial web site
~~~
wget https://github.com/prometheus/alertmanager/releases/download/v0.26.0/alertmanager-0.26.0.linux-amd64.tar.gz
~~~
## 4. Unarchive file that's we dowloded
~~~
tar -xvf <file.tar>
~~~
## To see what whas downloded use "ls" command
## Move bineries to "/user/local/bin"
~~~
sudo mv alertmanager /usr/local/bin/ 
~~~
~~~
sudo mv amtool /usr/local/bin/
~~~
## Add permission to user for folder
~~~
sudo chown alertmanager:alertmanager /usr/local/bin/alertmanager
~~~
## Make sure that we have right's to amtools 
~~~
sudo chown alertmanager:alertmanager /usr/local/bin/amtool
~~~
## And finally we need to move last file 
~~~
sudo mv alertmanager.yml /etc/alertmanager
~~~
## Give an permission for the folder
~~~
sudo chown -R alertmanager:alertmanager /etc/alertmanager/
~~~
## 5. Now we need to create a service alerrtmanager
~~~
sudo vim /etc/systemd/system/alertmanager.service
~~~
## And add config for the service
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
## 6. To start alertmanager we need make sure thats prometheus is not running
~~~
sudo systemctl stop prometheus
~~~
## Need to update prometheus.yml file 
~~~
sudo vim /etc/prometheus/prometheus.yml
~~~
## In the config file find Alertmanager config and replace "- alermanager:9093" with "localhost:9093"
## 7. Now we need to reload daemon
~~~
sudo systemctl daemon-reload
~~~
## And now let's start Prometheus and Alertmanager
~~~
sudo systemctl start prometheus
~~~
~~~
sudo systemctl start alertmanager
~~~
## And check that's all is running 
~~~
sudo systemctl status prometheus
~~~
~~~
sudo systemctl status alertmanager
~~~

