### PROMETHEUS GRAFFANA SETUP
```
refer following documentation for creating prometheus graffana configs
https://github.com/Vighnesh-99/Promethues-Grafana-Setup/blob/main/
https://github.com/AnupDudhe/Graffana-Prometheus/tree/main/Promethues-Grafana-Setup-main/Promethues-Grafana-Setup-main
https://www.linode.com/docs/guides/how-to-install-prometheus-and-grafana-on-ubuntu/
```
---------------------------------------------------------------------------------------------------------------

### download prometheus latest version from https://prometheus.io/download/  here you can download your node-exporter and prometheus as well.
```
sudo useradd --no-create-home prometheus
sudo mkdir /etc/prometheus
sudo mkdir /var/lib/prometheus
 ```
```
wget  https://github.com/prometheus/prometheus/releases/download/v2.54.1/prometheus-2.54.1.linux-amd64.tar.gz
tar -xvf prometheus-2.54.1.linux-amd64.tar.gz
sudo cp prometheus-2.54.1.linux-amd64/prometheus /usr/local/bin
sudo cp prometheus-2.54.1.linux-amd64/promtool /usr/local/bin
sudo cp -r prometheus-2.54.1.linux-amd64/consoles /etc/prometheus/
sudo cp -r prometheus-2.54.1.linux-amd64/console_libraries /etc/prometheus
#sudo cp prometheus-2.54.1.linux-amd64/promtool /usr/local/bin/
```
```
#rm -rf prometheus-2.54.1.linux-amd64.tar.gz prometheus-2.54.1.linux-amd64
sudo cp prometheus-2.54.1.linux-amd64/prometheus.yml /etc/prometheus/
sudo cp prometheus-2.54.1.linux-amd64/prometheus.service /etc/systemd/system/prometheus.service
```
```                                                                                               
sudo chown prometheus:prometheus /etc/prometheus
sudo chown prometheus:prometheus /usr/local/bin/prometheus
sudo chown prometheus:prometheus /usr/local/bin/promtool
sudo chown -R prometheus:prometheus /etc/prometheus/consoles
sudo chown -R prometheus:prometheus /etc/prometheus/console_libraries
sudo chown -R prometheus:prometheus /var/lib/prometheus
```
```
sudo systemctl daemon-reload
sudo systemctl enable prometheus
sudo systemctl start prometheus
sudo systemctl status prometheus
```
service file -:
```
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
Restart=on-failure
RestartSec=5s
ExecStart=/usr/local/bin/prometheus \
    --config.file /etc/prometheus/prometheus.yml \
    --storage.tsdb.path /var/lib/prometheus/ \
    --web.console.templates=/etc/prometheus/consoles \
    --web.console.libraries=/etc/prometheus/console_libraries \
    --web.listen-address=0.0.0.0:9090 \
    --web.enable-lifecycle \
    --log.level=info

[Install]
WantedBy=multi-user.target
```

### prometheus.yml file changes to add target/webserver nodes.
```
File: /etc/prometheus/prometheus.yml
...
- job_name: "remote_collector"
  scrape_interval: 10s
  static_configs:
    - targets: ["remote_addr:9100"]
```



--------------------------------------------------------------------------------------------------------
```
https://github.com/prometheus/node_exporter/releases/download/v1.8.2/node_exporter-1.8.2.linux-amd64.tar.gz
```
```
sudo useradd --no-create-home node_exporter

wget https://github.com/prometheus/node_exporter/releases/download/v1.8.2/node_exporter-1.8.2.linux-amd64.tar.gz
tar xzf node_exporter-1.8.2.linux-amd64.tar.gz
sudo cp node_exporter-1.8.2.linux-amd64/node_exporter /usr/local/bin/node_exporter
#rm -rf node_exporter-1.0.1.linux-amd64.tar.gz node_exporter-1.0.1.linux-amd64

sudo cp node-exporter.service /etc/systemd/system/node-exporter.service

sudo systemctl daemon-reload
sudo systemctl enable node-exporter
sudo systemctl start node-exporter
sudo systemctl status node-exporter
```
### nodeexporter service file :- 
```
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
Restart=on-failure
RestartSec=5s
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target
```

```
refer following documentation for creating prometheus graffana configs
https://github.com/Vighnesh-99/Promethues-Grafana-Setup/blob/main/
https://github.com/AnupDudhe/Graffana-Prometheus/tree/main/Promethues-Grafana-Setup-main/Promethues-Grafana-Setup-main
https://www.linode.com/docs/guides/how-to-install-prometheus-and-grafana-on-ubuntu/
```
------------------------------------------------------------------------------------------------------------------------
###graffana configuration and downloading 

download  graffana from this
```
link https://grafana.com/docs/grafana/latest/setup-grafana/installation/debian/  
```
```
systemctl status grafana-server
systemctl enable grafana-server
systemctl start grafana-server
systemctl restart grafana-server
systemctl status grafana-server
```
