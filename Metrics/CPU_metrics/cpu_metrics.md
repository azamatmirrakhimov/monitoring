# CPU metrics
## metrics of node cpu in Prometheus
~~~
node_cpu_guest_secods_total
~~~
and
~~~
node_cpu_seconds_total
~~~
# CPU Metrics
## - node_cpu prefix
## - Modes:
##	- idle: Timeidle
##	- lowait: Timewaiting for I/O
##	- irq: Time fixing interrups
##	- nice: Time spend on proccess with positive nicve value
##	- softirq: Time fixing interrups
##	- steal: ifVM, time stolen from CPU
##	- guest: ifhost, time spent for VM CPU cycles
##	- system: Time in the Kernel
## 	- user: Time in userland

## node_cpu_seconds_total
## 	- Counter: Adds time in each mode; always increse
##	- Use PromQL queries to extrac useful data
##	- rate: Used with counters to colculate the per-second average change in the given time series in the range
##	- irate: Same as rate, but for fast-moving counters, differences will be more obvious the lage time series
~~~
inrate(node_cpu_seconds_total[30s]) * 100
~~~
~~~
avg by (instance)(inrate(node_cpu_seconds_total{mode="user"}[30s])) * 100
~~~
