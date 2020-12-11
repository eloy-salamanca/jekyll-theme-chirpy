---
layout: post
comments: true
title: Latest updates to the Exchange Online Management PowerShell Module
excerpt: How to enable PowerShell remotely to run scripts
date: 2020-02-24 10:35:00 +0300
img: 11.1.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
category: powershell
tags: [PowerShell] # add tag
---

Lately, I had to execute Powershell very simple script on a large list of Windows systems, but lot of them weren't ready for it, so I ended up having to do some hacking, and previously checking if the system was ready to accept external commands.


https://office365itpros.com/2020/02/25/microsoft-updates-exchange-online-management-powershell-module/

```powershell
Import-Module ExchangeOnlineManagement -UseWindowsPowerShell
Connect-ExchangeOnline
```


After that, is it possible to try this:
```powershell
$WinRMEnabled = [bool](Test-WSMan -ComputerName $srv -ErrorAction SilentlyContinue)
If (!($WSManEnabled)) {
    .\PsExec.exe -h -u "user" -p "passwd" \\$server C:\Windows\System32\winrm.cmd quickconfig -quiet
}
```


![Enable Remote PowerShell]({{site.baseurl}}/assets/img/11.1.png)
