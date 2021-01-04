---
layout: post
comments: true
title: Configuring Remote Desktop listener certificate
excerpt: How to set Remote Desktop listener certificate to proper internal CA compatible certificate
date: 2021-01-04 11:47:20 +0300
img: 50.3.png
fig-caption: # Add figcaption (optional)
category: certificates
tags: [RDP, WindowsServer, Security]
---


For security reasons, I had to force the use of certificates delivered by our internal on RDP connections, and it was a pretty more straight forward process than I initially though.

## Requesting SSL certificate to the internal CA for Remote Desktop Authentication purposes

First of all, I need to request for the new certificate for the server:
![Requesting the certificate to the internal CA]({{site.baseurl}}/assets/img/50.1.png)

As I have templates in the Active Directory, I pick that as enrollment policy
![Active Directory enrollment policy]({{site.baseurl}}/assets/img/50.2.png)

Selected previously defined certificate template (only for Remote Desktop Authentication purposes) and click on **Properties* to define Common and Alternative name
![Properties on the certificate's template]({{site.baseurl}}/assets/img/50.4.png)

![Setting up Common and Alternative Name]({{site.baseurl}}/assets/img/50.5.png)

To verify everything worked as expected, press on **Start** **Run** and type `certlm.msc`
A new nice SSL certificate, CA internal compatible has been released.
![opening certlm.msc]({{site.baseurl}}/assets/img/50.6.png)
![Checking for the new certificate]({{site.baseurl}}/assets/img/50.6.png)

---

## Pointing Remote Desktop listener to the new certificate

Last and not least, I had to move the Remote Desktop listener to the new certificate, easy-peasy process, and as I like powershell above all, I decided to carry on everything from it

### Get Digital Thumbprint of the certificate
Open Powershell and type the following: `Get-ChildItem cert:\LocalMachine\My`
Copy the Thumbprint
![getting the Digital Thumbprint]({{site.baseurl}}/assets/img/50.8.png)

### Modify the Remote Desktop listener
Using that thumbprint, roll out the following, substituting appropiate Thumbprint
`wmic /namespace:\\root\cimv2\TerminalServices PATH Win32_TSGeneralSetting Set SSLCertificateSHA1Hash="THUMBPRINT"`
![Modifying Remote Desktop Listener]({{site.baseurl}}/assets/img/50.9.png)

---

## Testing new behaviour
First of all, you will need to delete historic session to the server you will like to test; to do so, simply open `regedit` and go to `HKEY_CURRENT_USER\Software\Microsoft\Terminal Server Client\Servers\`; after that delete the entire folder related to the server or IP.

Once you have done this, simple open new RDP to the server and you shouldn't receive any warning for incoming new connection the server, as your computer trust on it.
