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
   <li>1. Prometheus Server</li>
   <li>2. Service Discovery</li>
   <li>3. Scrape Target</li>
   <li>4. Alert Manager</li>
   <li>5. User Interface</li>
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

~ sudo apt update -y

## Step #1 : Creating Prometheus System Users and Directory

### Create a system user for Prometheus using below commnds :

~ sudo useradd --no-create-home --shell /bin/false prometheus

### Create the directories in which we will be storing our configuration files and libraries :

~ sudo mkdir /etc/prometheus
~ sudo mkdir /var/lib/prometheus

## Step #2 : Download Prometheus Binary File

### Using below command we can download Prometheus, here we are downloading Prometheus 2.46 version, you use above link to download specific version.

### You need to go inside /tmp dir :

~ cd /tmp/

### Download the Prometheus setup using wget

~ wget https://github.com/prometheus/prometheus/releases/download/v2.46.0/prometheus-2.46.0.linux-amd64.tar.gz

### Extract the files using tar :

~ tar -xvf prometheus-2.46.0.linux-amd64.tar.gz

### Move the configuration file and set the owner to the prometheus user :

~ cd prometheus-2.46.0.linux-amd64

~ sudo mv console* /etc/prometheus

~ sudo mv prometheus.yml /etc/prometheus

~ sudo chown -R prometheus:prometheus /etc/prometheus
