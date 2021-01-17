---
layout: post
comments: true
title: Jekyll Test Blog on Ubuntu Guest VM on top of Hyper-V
excerpt: How to create Jekyll Test Blog on Ubuntu Guest VM on top of Hyper-V
date: 2020-11-20 08:59:00 +0300
img: 49.1.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
category: [virtualization]
tags: [ubuntu, virtualization, hyper-v] # add tag
---

Wanted to change blog look and feel but didn't like the idea of touching any "productive" settings and miss something, so I decided to search for a way to set it up locally and then reply all changes to [GitHub Pages](https://pages.github.com/) at once. This is how I did step by step, because I had some difficulties in the journey.

---

## Prerequisites
To make a long history short, I will start from the following assumptions:
1. Hyper-V Server properly set and configured (I used my W10 laptop)
2. Ubuntu Server 20.04 LTS as guest VM properly set and updated

---

## Networking Sets
I wanted guest vm to be internet connected and to the Hyper-v host at the same time, and it wasn't not so easy at it promised, but I got it this way:

1. Defined new Hyper-V virtual switch, external network
![Hyper-V virtual switch external]({{site.baseurl}}/assets/img/49.1.png)

2. Configuring new network interface on the host created after new virtual switch
![Configuring Network interface]({{site.baseurl}}/assets/img/49.2.png)

3. Line the guest on the same network
```
 sudo nano /etc/netplan/00-installer-config.yaml
```
![Lining the guest]({{site.baseurl}}/assets/img/49.3.png)

---

## Sharing Jekyll Directory
As I had to modify files as easy as possible, I shared W10 directory yo access from Ubuntu:
![W10 directory]({{site.baseurl}}/assets/img/49.4.png)

![W10 directory permissions]({{site.baseurl}}/assets/img/49.5.png)

---

## Mounting shared folder on Ubuntu
First of all, need cifs client to access shared folder:
```
$ sudo apt install cifs-utils
```
![Install cifs client]({{site.baseurl}}/assets/img/49.6.png)

Created new folder:
```
mkdir ~/jekyll-theme-chirpy
```
And mounted the shared folder:
```
sudo mount.cifs //SURFASAURUS/jekyll-theme-chirpy ~/jekyll-theme-chirpy -o user=ubuntu
```
![Mounting shared folder]({{site.baseurl}}/assets/img/49.6.png)

