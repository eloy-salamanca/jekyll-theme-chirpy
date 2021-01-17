---
layout: post
comments: true
title: Useful PowerShell Snippets for SysAdmins
excerpt: Sometimes I need to re-use old PowerShell snippets, but I had difficulties 
date: 2018-04-18 17:39:00 +0300
img: 18.5.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
category: [powershell]
tags: [PowerShell, Sysadmin] # add tag
---

Sometimes I need to re-use old PowerShell snippets, but I had difficulties to find it out again, so it might be a good idea to put all of this here.

## 1.Connecting to remote hosts without dropping passwords clear text inside scripts
First thing, I encrypted the password in a text file for later use, by


![Encrypting the passwords]({{site.baseurl}}/assets/img/18.1.png)

```powershell
Read-Host -prompt "Enter password to be encrypted in mypassword.txt" -assecurestring | Convertfrom-securestring | Out-File '.\securestring.txt'
```

This way, I can connect to remote systems without having to specify clear passwords, like this:

![Encrypting the passwords]({{site.baseurl}}/assets/img/18.2.png)

```powershell
$pass = cat '.\securestring.txt' | convertto-securestring
$mycred = new-object -typename System.Management.Automation.PSCredential -argumentlist "Admin@domain",$pass
```

![Connecting to remote systems]({{site.baseurl}}/assets/img/18.3.png)


## 2.Copy files using BITS

Copy big files between systems without affecting too much to network performance or consuming bandwidth it's a very important thing, and I had good results using BITS, like below example:

```powershell
Import-Module BitsTransfer
Start-BitsTransfer -Source $Source -Destination $Destination -DisplayName "Transferring file"
```

![Transferring file example]({{site.baseurl}}/assets/img/18.4.png)

You can even wait until finishing the copy

![Coding example]({{site.baseurl}}/assets/img/18.5.png)

```powershell
Import-Module BitsTransfer
# Start the BITS transfer. Added a loop to wait until complete
$job = Start-BitsTransfer -Source $Source -Destination $Destination -Asynchronous -DisplayName "Transferring file"
While ($job | Where-Object { $job.JobState -eq "Transferring"}) {
    Sleep -Seconds 1
}
```

![Running script]({{site.baseurl}}/assets/img/18.6.png)
