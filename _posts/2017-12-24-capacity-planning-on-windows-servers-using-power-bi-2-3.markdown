---
layout: post
comments: true
title: Capacity Planning on windows Servers using Power BI 2
excerpt: How to enable PowerShell remotely to run scripts
date: 2017-12-24 19:46:00 +0300
img: 39.1.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
category: [powershell]
tags: [PowerShell, Capacity Plan, SysAdmin] # add tag
---

Once our db is set and properly running, next step is to deploy the agent on intended servers.

Our goal is to schedule ps script and get it running daily on different time windows, by default: 2am, 10am, 4pm; and thus measuring from high business loads to lower, so we can compare how our servers are working.

After launched and reached one server, script will ask for computer information (processors, license, OS version, etc) and will push all of this in different tables (DiskPeaksCAP, ServerCAP, ServerNICsCAP, ServerPeaksCAP):

* **Set-ServerCapRep.ps1**

Then, it will copy following agent script, and finally schedule to run 3 times on a daily basis.
* **Add-DataServerPeakAgent.ps1**

You only need an input text file, containing list of servers you want to deploy agents. It should go with the rest of scripts and be named as **Servers.txt**

This is an example of what you can expect after running:

```powershell
.\Set-ServerCapRep.ps1 -file .\Servers.txt -verbose
```

![Running script]({{site.baseurl}}/assets/img/39.1.png)

You can also check for data with [SQL Operations Studio](https://eloysalamanca.es/sql/testing-sql-operations-studio), just to make sure you’ve got all sorted.

![SQL Operations Studio]({{site.baseurl}}/assets/img/39.2.png)
