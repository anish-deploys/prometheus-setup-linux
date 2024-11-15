# Prometheus Toolkit Setup Linux

## What is Prometheus ?
<ul>
  <li>Prometheus is a open source Linux Server Monitoring tool mainly used for metrics monitoring, event monitoring, alert management, etc.</li>
  <li>Prometheus has changed the way of monitoring systems and that is why it has become the Top-Level project of Cloud Native Computing Foundation (CNCF).</li>
  <li>Prometheus uses a powerful query language i.e. “PromQL”.</li>
  <li>In Prometheus tabs are on and handles hundreds of services and microservices.</li>
  <li>Prometheus use multiple modes used for graphing and dashboarding support.</li>
</ul>

## Prometheus Architecture

 ![prom](https://github.com/user-attachments/assets/0b97ce7e-71d7-47a5-9326-cc526e5493c2)

 ## Prometheus Components
 <ul>
   <li>Prometheus Server</li>
   <li>Service Discovery</li>
   <li>Scrape Target</li>
   <li>Alert Manager</li>
   <li>User Interface</li>
 </ul>

## Prerequisites
<ul>
  <li>Ubuntu with 22.04 Version</li>
  <li>Root user account with sudo  privilege.</li>
  <li>Prometheus system user and group.</li>
  <li>Sufficient storage on your system and good internet connectivity.</li>
  <li>Ports Required- 9090 (Prometheus), 3000 (Grafana), 9100 (Node Exporter)</li>
</ul>

### We will update the system repository index by using the following command.

    sudo apt update -y

## Step #1 : Creating Prometheus System Users and Directory

### Create a system user for Prometheus using below commnds :

    sudo useradd --no-create-home --shell /bin/false prometheus

### Create the directories in which we will be storing our configuration files and libraries :

    sudo mkdir /etc/prometheus
    sudo mkdir /var/lib/prometheus

## Step #2 : Download Prometheus Binary File

### Using below command we can download Prometheus, here we are downloading Prometheus 2.46 version, you use above link to download specific version.

### You need to go inside /tmp dir :

    cd /tmp/

### Download the Prometheus setup using wget

    wget https://github.com/prometheus/prometheus/releases/download/v2.46.0/prometheus-2.46.0.linux-amd64.tar.gz

### Extract the files using tar :

    tar -xvf prometheus-2.46.0.linux-amd64.tar.gz

### Move the configuration file and set the owner to the prometheus user :

    cd prometheus-2.46.0.linux-amd64

    sudo mv console* /etc/prometheus

    sudo mv prometheus.yml /etc/prometheus

    sudo chown -R prometheus:prometheus /etc/prometheus

### Move the binaries and set the owner :

    sudo mv prometheus /usr/local/bin/

    sudo chown prometheus:prometheus /usr/local/bin/prometheus

## Step #3 : Prometheus configuration file

### We have already copied /opt/prometheus-2.26.0.linux-amd64/prometheus.yml file /etc/prometheus directory, verify if it present and should look like below and modify it as per your requirement.

    sudo nano /etc/prometheus/prometheus.yml

Enter this code and Ctrl + S to save and Ctrl + X to exit

    [Unit]
    Description=Prometheus
    Wants=network-online.target
    After=network-online.target

    [Service]
    User=prometheus
    Group=prometheus
    Type=simple
    ExecStart=/usr/local/bin/prometheus \
        --config.file /etc/prometheus/prometheus.yml \
        --storage.tsdb.path /var/lib/prometheus/ \
        --web.console.templates=/etc/prometheus/consoles \
        --web.console.libraries=/etc/prometheus/console_libraries
        --web.listen-address=0.0.0.0:9090  
    Restart=always
    RestartSec=10s
    [Install]
    WantedBy=multi-user.target

### Reload systemd :

    sudo systemctl daemon-reload

### Start, Enable, Status Prometheus service :

    sudo systemctl start prometheus
    sudo systemctl enable prometheus
    sudo systemctl status prometheus

## Step #5 : Accessing Prometheus in Browser

### Now as Prometheus installation and configuration is set up and it is ready to use we can access  its services via web interface.Also check weather port 9090 is UP in firewall.
### Use below command to enable prometheus service in firewall 

    sudo ufw allow 9090/tcp

### Now Prometheus service is ready to run and we can access it from any web browser.

    http://localhost:9090
    


