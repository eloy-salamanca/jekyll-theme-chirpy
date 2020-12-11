---
layout: post
comments: true
title: Preparing to use Docker and Docker Compose from Windows 10 WSL
excerpt: See how to prepare your Docker on Windows 10 installation to use on WSL, including docker-compose
date: 2019-05-02 14:30:00 +0300
img: 30.8.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
category: docker
tags: [Docker, docker-compose, Hyper-V, Linux, Windows 10, WSL] # add tag
---

Now that I'm trying to experiencing with Microservices, I wanted to use my Windows 10 Surface Pro laptop, and see whether it's possible to play with using WSL or not, just to create my lab environment

---

## Installing WSL
WSL (**Windows Subsystem for Linux**), is the easy way of having linux on top of my Windows 10, so it's perfect to use linux only related stuff.

As I've got one of the latest versions of Windows 10 (1809), I was able to install WSL the easy way:

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

![Enabling WSL]({{site.baseurl}}/assets/img/30.1.png)

Then, I installed latest Linux Ubuntu version from Microsoft Store

![Installing WSL]({{site.baseurl}}/assets/img/30.2.png)

Afterward, setting up my new Linux user out of the box

![Checking WSL installation]({{site.baseurl}}/assets/img/30.3.png)

---

## Install Docker and Docker-Compose
As I had a Docker for Windows installation already configured, I only had to tweak it a bit and get it ready to use from WSL:

![Install Docker and Docker-Compose]({{site.baseurl}}/assets/img/30.4.png)

Going to WSL to install Docker

```bash
wget -qO- https://get.docker.com/ | sh
```

![Installing Docker on WSL]({{site.baseurl}}/assets/img/30.5.png)

Also, Docker Compose, including all requirements

```bash
sudo apt-get update
sudo apt-get -y install python-pip
sudo pip install docker-compose
```

![Installing Docker-Compose and dependencies on WSL]({{site.baseurl}}/assets/img/30.6.png)

And after that, liked to verifying that Docker and Docker-Compose were correctly installed

```bash
docker info
docker-compose --version
```

![Checking installation]({{site.baseurl}}/assets/img/30.7.png)

---

## Interconnect Docker for Windows and WSL
One liner, available everytime WSL start

```bash
echo "export DOCKER_HOST=tcp://localhost:2375" >> ~/.bashrc && source ~/.bashrc
```

Et voilà! easy peasy! See available Docker from WSL!

![Testing everything]({{site.baseurl}}/assets/img/30.8.png)
