---
layout: post
comments: true
title: Enabling Remote PowerShell from Script on earlier and new PowerShell versions
excerpt: How to enable PowerShell remotely to run scripts
date: 2017-12-19 10:27:00 +0300
img: 37.9.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
category: nanoserver
tags: [PowerShell, nanoserver, Cluster] # add tag
---

https://aka.ms/exops-docs


```powershell
Connect-ExchangeOnline -EnableErrorReporting -LogDirectoryPath <Path to store log file> -LogLevel All
```


```powershell
Install-Module PowershellGet -Force
```

```powershell
Update-Module PowershellGet
```

```powershell
Install-Module -Name ExchangeOnlineManagement
```

To see the version of the EXO V2 module 
```powershell
Import-Module ExchangeOnlineManagement; Get-Module ExchangeOnlineManagement
```

To update EXO V2 module to the latest versions available in the PowerShell Gallery
```powershell
Update-Module -Name ExchangeOnlineManagement
```

To confirm that the update was successful, run the following commands:
```powershell
Import-Module ExchangeOnlineManagement; Get-Module ExchangeOnlineManagement
```

Uninstall the module
```powershell
Uninstall-Module -Name ExchangeOnlineManagement
```

Connect to Exchange Online using EXO V2 module
```powershell
$UserCredential = Get-Credential
# Without MFA enabled
Connect-ExchangeOnline -Credential $UserCredential -ShowProgress $true
# With MFA enabled
Connect-ExchangeOnline -UserPrincipalName <UPN> -ShowProgress $true
```


Use this cmdlet to view the settings of content filter policies in your cloud-based organization
```powershell
Get-HostedContentFilterPolicy | Format-List
```

To check rules applied to emails identified as SPAM
```powershell
Get-HostedContentFilterPolicy | Select-Object PhishSpamAction, RedirectToRecipients | Format-List
```
---

```powershell
Connect-IPPSSession -UserPrincipalName <your UPN>
```


![Import Module]({{site.baseurl}}/assets/img/37.1.png)

