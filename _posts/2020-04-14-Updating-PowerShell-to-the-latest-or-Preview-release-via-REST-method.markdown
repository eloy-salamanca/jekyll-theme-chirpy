---
layout: post
comments: true
title: Updating PowerShell to the latest or Preview release via REST method
excerpt: How to upgrade PowerShell to the last version throughout internet
date: 2020-04-14 11:10:00 +0300
img: 43.1.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
category: powershell
tags: [PowerShell] # add tag
---

* Latest stable version:
```powershell
Invoke-Expression "& { $(Invoke-RestMethod 'https://aka.ms/install-powershell.ps1') }"
```

* Latest Preview version
```powershell
Invoke-Expression "& { $(Invoke-RestMethod 'https://aka.ms/install-powershell.ps1') } -UseMSI -Preview"
```

![Updating PowerShell to Preview release]({{site.baseurl}}/assets/img/43.2.png)
