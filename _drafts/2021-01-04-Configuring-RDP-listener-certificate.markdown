---
layout: post
comments: true
title: Configuring Remote Desktop listener certificate
excerpt: How to set Remote Desktop listener certificate to proper internal CA compatible certificate
date: 2021-01-04 11:47:20 +0300
img: 50.1.png
fig-caption: # Add figcaption (optional)
category: certificates
tags: [RDP, WindowsServer, Security]
---

Lately, I had to execute Powershell very simple script on a large list of Windows systems, but lot of them weren't ready for it, so I ended up having to do some hacking, and previously checking if the system was ready to accept external commands.


After that, is it possible to try this:
```powershell
$WinRMEnabled = [bool](Test-WSMan -ComputerName $srv -ErrorAction SilentlyContinue)
If (!($WSManEnabled)) {
    .\PsExec.exe -h -u "user" -p "passwd" \\$server C:\Windows\System32\winrm.cmd quickconfig -quiet
}
```


![Enable Remote PowerShell]({{site.baseurl}}/assets/img/11.1.png)
