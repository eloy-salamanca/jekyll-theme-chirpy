---
layout: post
comments: true
title: Linux equivalent of WSUS
excerpt: Using internet connected Ansible Server to update offline Linux Servers
date: 2021-04-12 12:13:00 +0300
img: 51.1.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
category: ansible
tags: [security, ansible, linux] # add tag
---

As I had to define new monitoring system from scratch, and now testing how InfluxDB, Telegraf and Grafana performs on a on-premises environment.

- **InfluxDB** > InfluxDB is an Open Source Time Series Database Platform for storing Time Series Data or what we are looking for: metrics & Events collected from different devices
- **Telegraf** > Agent written in Go for collecting performance metrics from the system it’s running on and the services running on that system. Collected metrics can be sink into InfluxDB.
- **Grafana** > Grafana is an open source, feature rich metrics dashboard and graph editor for Graphite, Elasticsearch, OpenTSDB, Prometheus, and InfluxDB. As an example, when using InfluxDB as your data source, data stored on InfluxDB will be visualized using Grafana Graphs.

* [Prerequisites](#prerequisites)
* [InfluxDB](#influxdb)
* [Grafana](#grafana)

---

<div id='prerequisites' />

## Prerequisites

- Ubuntu 20.4 Linux Server
- Docker and docker-compose, latest versions

---

Install Squid
sudo apt update
sudo apt install squid

Test configuration
netstat -plunt | grep 3128

Backup original file
sudo cp /etc/squid/squid.conf{,.ori}

sudo nano /etc/squid/squid.conf


By default, squid is set to listen on port 3128 on all network interfaces on the server, so change to the following
```
# Squid normally listens to port 3128
http_port IP_ADDR:PORT
```

Create new file with IP Addresses
sudo nano /etc/squid/allowed_hosts.txt

Put inside allowed hosts
host1
host2
...

Create new acl in squid.conf to allow access to defined hosts


Allow access to http for defined hosts

Allos access to https for defined hosts

restart squid
systemctl restart squid

Allow corporate firewalls connections TCP/8080 from allowed hosts

---

Each host, do the following `sudo nano /etc/apt/apt.conf.d/05proxy`
```
Acquire {
  HTTP::proxy "http://esse1-dops-21.brenntag-iberia.com:8080";
  HTTPS::proxy "http://esse1-dops-21.brenntag-iberia.com:8080";
}
```
