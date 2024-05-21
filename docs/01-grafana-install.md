# Установка `Grafana`
## 1. Установка системы с официального сайта 
~~~
https://grafana.com/grafana/download
~~~
~~~
sudo apt-get install -y adduser libfontconfig1 musl
~~~
~~~
wget https://dl.grafana.com/enterprise/release/grafana-enterprise_11.0.0_amd64.deb
~~~
~~~
sudo dpkg -i grafana-enterprise_11.0.0_amd64.deb
~~~
## На этом `Grafana` установилась и только осталось перезапустить `daemond`
## `daemon service`
~~~
systemctl daemon-reload
~~~
~~~
systemctl enable grafana
~~~
~~~
systemctl enable grafana
~~~
~~~
systemctl start grafana
~~~
~~~
systemctl status grafana
~~~
~~~
netstat -tunlp
~~~
