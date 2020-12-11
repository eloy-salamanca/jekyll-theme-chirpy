---
layout: post
comments: true
title: Security tip Disable PowerShell 2 0 engine in latest Windows 10 Builds
excerpt: It does not make a lot of sense having different PowerShell versions at the same time, how to remove PowerShell 2.0 and avoid security risks.
date: 2019-06-14 07:24:00 +0300
img: 33.1.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
category: powershell
tags: [PowerShell, Windows 10] # add tag
---

The less old stuff you have in your system, the more secure you will be; it doesn’t make a lot of sense having different PowerShell versions in your computer at the same time, so you’d better remove PowerShell 2.0 as soon as possible and avoid security risks.

This is and easy to do it, by the way using latest PowerShell 7.0.0 preview-1, as you can see at the screenshot

## Check current status
```powershell
Get-WindowsOptionalFeature -Online -FeatureName MicrosoftWindowsPowerShellV2
```

## Disabling PowerShell 2.0
```powershell
Disable-WindowsOptionalFeature -Online -FeatureName MicrosoftWindowsPowerShellV2Root
```

![Disabling PowerShell 2.0]({{site.baseurl}}/assets/img/33.1.png)
