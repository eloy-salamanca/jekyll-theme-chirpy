---
layout: post
comments: true
title: Working with PowerShell Repositories
excerpt: Important to keep our work with PowerShell repositories, keeping them updated to the latest and to avoid bugs
date: 2019-10-01 15:49:00 +0300
img: 34.1.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
category: [powershell]
tags: [PowerShell, PowerShell7, IaaC, NuGet, Orquestration, PowerShell Gallery] # add tag
---

Package Management is becoming more and more important these days to keep the ball rolling; this is a first approach on working with PowerShell Repositories, using **NuGet Gallery** and latest [PowerShell v7.0.0-preview4](https://github.com/PowerShell/PowerShell/releases)


PowerShell7 comes with `PackageManagement` Module, which is basic for my purpose:
```powershell
Get-Command -Module PackageManagement
```

Also, **NuGet** and **PowerShell Gallery** are included:
```powershell
Get-PackageSource
```

To know further details about a particular repository:
```powershell
Get-PSRepository -Name "PSGallery" | Format-List * -Force
```

Last but not least, important to keep modules updated (not applicable in this example)
```powershell
Update-Module
```

![Working with PowerShell Repositories]({{site.baseurl}}/assets/img/34.1.png)
