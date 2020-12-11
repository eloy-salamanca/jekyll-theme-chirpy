---
layout: post
comments: true
title: Monitoring on-premises workloads using Prometheus and Grafana
excerpt: Step by step guide to install and configure Linux Server to monitor on-premises workloads with Prometheus and Grafana
date: 2020-08-11 09:18:00 +0300
img: 46.1.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
category: monitoring
tags: [monitoring, prometheus, grafana, linux] # add tag
---

As I had to define new monitoring system from scratch, and wanting to see how Prometheus and Grafana behaves on a on-premises environment, I decided to set up Linux Server and put everything into it. This was the trip that I took:

* [Prerequisites](#prerequisites)
* [Prometheus](#prometheus)

---

## Prerequisites

- Ubuntu 20.4 Linux Server
- Docker and docker-compose, latest versions

---

## Prometheus
Installed Prometheus as suggested on [Prometheus GitHub](https://github.com/prometheus/prometheus)
```
docker run --name prometheus -d -p 9090:9090 prom/prometheus
```
After that, Prometheus should be up and running, and accessible from browser in the LAN
![Prometheus Start Page]({{site.baseurl}}/assets/img/46.1.png)

---

### Grafana
Installed Prometheus as suggested on [Graphana docs](https://grafana.com/docs/grafana/latest/installation/docker/)
```
sudo docker run -d -p 3000:3000 grafana/grafana
```

Graphana also up and ready
![Grafana Start Page]({{site.baseurl}}/assets/img/46.2.png)

---

### vmware_exporter
It is a VMware vCenter Exporter for Prometheus. As I had different VMware vCenter and ESXi nodes, I wanted to use config file, so it was not possible to use docker image (it only use variables)

config.yml example:

```config.yml
default:
    vsphere_host: "vcenter"
    vsphere_user: "user"
    vsphere_password: "password"
    ignore_ssl: True
    specs_size: 5000
    fetch_custom_attributes: True
    fetch_tags: True
    fetch_alarms: True
    collect_only:
        vms: True
        vmguests: True
        datastores: True
        hosts: True
        snapshots: True

esx:
    vsphere_host: vc.example2.com
    vsphere_user: 'root'
    vsphere_password: 'password'
    ignore_ssl: True
    specs_size: 5000
    fetch_custom_attributes: True
    fetch_tags: True
    fetch_alarms: True
    collect_only:
        vms: False
        vmguests: True
        datastores: False
        hosts: True
        snapshots: True
```

Install process:
```
sudo pip3 install vmware_exporter

