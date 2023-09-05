# Install node exporter
## 1. Step create user
~~~
sudo useradd --no-create-home --shell /bin/false node_exporter
~~~
## 2. So we need do dowload nessery files from Prometeus dowload page
~~~
wget https://github.com/prometheus/node_exporter/releases/download/v1.6.1/node_exporter-1.6.1.linux-amd64.tar.gz
~~~
## Unarchive file
~~~
tar -xvf node_exporter-1.6.1.linux-amd64.tar.gz
~~~
## And move to the unarchive directory
~~~
cd node_exporter-1.6.1.linux-amd64
~~~
## Only one file we need to move to binery
~~~
sudo mv node_exporter /usr/local/bin/
~~~
## And olso we need to give an permission to file
~~~
chown node_exporter:node_exporter /usr/local/bin/
~~~
## 3. So we need to create systemd file now 
~~~
sudo vim /etc/systemd/system/node_exporter.service
~~~
## In the file we need write service file
~~~
[Unit]
Description=Node Exporter
After=network.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target
~~~
## 4. Start service
~~~
sudo systemctl daemon-reload
~~~
~~~
sudo systemctl enable node_exporter
~~~
~~~
sudo systemctl start node_exporter
~~~


