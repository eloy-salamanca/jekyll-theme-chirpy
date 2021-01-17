---
layout: post
comments: true
title: Playing with Project Honolulu Technical Preview 1802
excerpt: New features and improvements of Honolulu Microsoft Project Preview 1802
date: 2018-04-18 06:28:20 +0300
img: 13.7.png # Add image post (optional)
category: [SysAdmin]
tags: [Honolulu, Windows Admin Center, Windows Server]
---
Last **February, 13th** new preview of Honolulu Project was released for Windows Insiders, along with new few interesting features and improvements were added, so it's time to check it, as future Windows Server 2018 looks will take advantage of it, and probably we'll use Honololu a lot in the near future.

To check full list of changes and improvements, check [Announcing Windows Server Insider Preview Build 17093](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver)

To download Honolulu Project Technical Preview 1802, as well as Windows Insider Preview Build 17093, check [Windows Server Insider Preview download page](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver)

Let's see installation process and new features:

## Install
![Install1]({{site.baseurl}}/assets/img/13.1.png)
![Install2]({{site.baseurl}}/assets/img/13.2.png)
![Install3]({{site.baseurl}}/assets/img/13.3.png)
![Install4]({{site.baseurl}}/assets/img/13.4.png)

## Connections Panel
New **gear icon** in the upper right of the windows, linking to extension manager and more:
![Connections1]({{site.baseurl}}/assets/img/13.5.png)
<br>
In Server Manager solution, some detection logic has been added, for example, when Hyper-V role detected, the ability to manage Virtual Machines or Virtual Switches, as you can see here:
<br>

## Server Manager
![Server Manager1]({{site.baseurl}}/assets/img/13.6.png)
![Server Manager2]({{site.baseurl}}/assets/img/13.7.png)
![Server Manager3]({{site.baseurl}}/assets/img/13.8.png)
*Is not that incredible to manage a lot of settings without having to install or switch in between tons of consoles?*

2 more interesting features, as appears in original announcement:<br>

> ## High-Availability
> You can now deploy Project Honolulu in a failover cluster for high availability of your Honolulu gateway service. We’ve provided 3 PowerShell scripts that enable you to easily install, update, or uninstall Project Honolulu onto an existing failover cluster. You’ll need a Cluster Shared Volume to persist data across the cluster, but the scripts will install Project Honolulu and configure certificates on all the nodes. By deploying Project Honolulu on a failover cluster, you can ensure that you are always able to manage the servers in your environment. See the [HA deployment guide](https://aka.ms/HonoluluHASetup) for setup instructions and link to the scripts.<br>
> ## Settings - Access
>This section only applies when you are running Honolulu as a service on Windows Server. Here you can define security groups (either Active Directory, or local machine groups) for both user and administrator access to Honolulu.
>Previously, to access the Honolulu service, users were required to have logon access on the gateway machine. Now you can configure your environment in such a way that users can access the Honolulu service without the rights to log on to the gateway machine.<br>

> The default behavior is unrestricted; any user that navigates to the gateway URL will have access to the Honolulu interface. Once you add one or more security groups to the users list, access is restricted to the members of those groups. If you want to enforce the use of **smartcard authentication**, you can specify an additional requiredgroup for smartcard-based security groups. In this case, a user will have access if they are in any security group **AND** a smartcard group.<br>

> On the Administrators tab, you define the security groups that will have privileges to change Honolulu settings. Smartcard groups work the same way here as for the user list. The local administrators group on the gateway machine will always have full administrator access and cannot be removed from the list. The administrators list supports the same AND condition for smartcards groups as the users list.

## Remote Desktop
Of course, daily useful tools in front of us:
![Remote Desktop]({{site.baseurl}}/assets/img/13.9.png)

## Windows Update
![Windows Update]({{site.baseurl}}/assets/img/13.10.png)

## PowerShell
![Remote Desktop]({{site.baseurl}}/assets/img/13.11.png)
