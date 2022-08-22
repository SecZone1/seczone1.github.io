---
title:  " Make Active Directory vulnerable  "
layout: post
category: Active-Directory
tags: [AD, Windows-server]
excerpt: " "
---


Download Script ->  **[vulnerable-AD](https://github.com/WazeHell/vulnerable-AD)**

#  Main Features
-   Randomize Attacks
-   Full Coverage of the mentioned attacks
-   you need run the script in DC with Active Directory installed
-   Some of attacks require client workstation

##  Supported Attacks

-   Abusing ACLs/ACEs
-   Kerberoasting
-   AS-REP Roasting
-   Abuse DnsAdmins
-   Password in Object Description
-   User Objects With Default password (Changeme123!)
-   Password Spraying
-   DCSync
-   Silver Ticket
-   Golden Ticket
-   Pass-the-Hash
-   Pass-the-Ticket
-   SMB Signing Disabled


# Run Script 

- open powershell on Active Directory 

![Desktop View](/assets/img/AD_Lab/p.png){: }

-  run this command 

```bash
# access script dir -> I Download script at desktop
. .\vulnad.ps1
Invoke-VulnAD -UsersLimit 100 -DomainName "homelab.local"

```
Replace Homelab.local  with the name of your Domain.

- After that you should see the following output:

![Desktop View](/assets/img/AD_Lab/Pasted image 20220821052304.png){: }

![Desktop View](/assets/img/AD_Lab/Pasted image 20220821052347.png){: }


And you have successfully set up your vulnerable AD!
