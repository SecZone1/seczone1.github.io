---
title: "Introduction And Scenario of create Active Directory Lab "
layout: post
category: Active-Directory
tags: [AD, Windows-server]
excerpt: " "
---


# INTRODUCTION
## Brief Overview of Microsoft’s Active Directory  
Active Directory is a directory service provided by Microsoft that is commonly implemented within organizations for structuring and networking purposes. Active Directory, often abbreviated as AD, uses a secure hierarchical containment structure called logical structure, allowing administrators to organize objects into a hierarchical collection of containers. Additionally, Microsoft’s Active Directory offers a number of authentication and authorization solutions that allow organizations to organize their network and resources. To put it simply, Active Directory allows administrators to create and manage resources, users, domains and other objects within a network. For instance, a network administrator may create a group of users and provide them with permissions to a specific resource within a network.

## Active Directory Attacks and Defence  
Microsoft’s Active Directory remains a primary directory service solution within organisations’ networks. It is vital for companies to understand and identify potential security weaknesses of Active Directory, as it remains a major pivot point utilized by cybercriminals to compromise organisations worldwide, including governments and companies. In order to detect security threats and remediate vulnerabilities, understanding the prevalent Active Directory attack techniques and threats they pose to organisations is critical. In this section of the introduction, a brief background into the attacks against Active Directory environments is provided. Typically, a high-skilled and well-organized Active Directory attack consists of multiple phases as it can be seen in the figure below:

![Desktop View](/assets/img/AD_Lab/1 (1).png){: }


As demonstrated in the figure above, phishing is a key phase in an Active Directory attack that may lead to a victim providing sensitive information to the attacker or installing malicious software. That way, a perpetrator can gain a foothold inside of an organisation’s internal network and carry out further attacks.  
Following that, an attacker performs enumeration to increase the attack surface by discovering valuable information about the deployed environment, and potentially retrieve sensitive user data. As credential theft is carried out, it may be used to carry out exploitation attacks against the authentication and authorization systems inside the network. Additionally, a perpetrator may discover implemented vulnerable software and perform exploitation attacks against it to gain further access within the network. As an attacker gains access to any accessible entity, such as a low-privileged user, they can perform privilege escalation techniques in order to move laterally and vertically across the Active Directory network to gain access to valuable assets, such as confidential data, high-privileged accounts and more. As a final stage of the attack, a malicious insider may perform various techniques in order to obtain persistence within the network.  

In summary, Active Directory is a widely adopted and useful technology solution for managing complex resources and corporate networks. As explained earlier, Active Directory holds a large and complex attack surface and, therefore, is a major pivot point for cybercriminals to compromise companies. Additionally, as the Active Directory is a critical application, dealing with various sensitive data, within the majority of enterprises, it is vital to increase its security and understand the potential security threats it raises. Providing staff with learning material and training environments is a great approach to learn more about the security of various technologies, including the Active Directory. One of the ways to gain experience  
and learn Active Directory security is to understand the attacking techniques by performing them in a virtual environment. In addition, lab environments are a great way to learn about the modern techniques and tools used by cybercriminals.


# The Scenario  
![Desktop View](/assets/img/AD_Lab/1 (2).png){: }

The lab consists of five lab machines, including the pfSense (Router) , Domain Controller and three client machines. And Scenario : 
-  Install PfSense (Router) with Two Network WAN  connect to ISP and LAN internal network . The lab environment network’s subnet address is set to 192.168.1.0/24
-  Install Windows Server 2019 and config DC [Homelab.Local] 
-  Create User three Users. 
-  join the machines to DC  
-  run [vulnerable-AD](https://github.com/WazeHell/vulnerable-AD) script to make DC vulnerable 

## Requirements  
 -  PfSense as router , windows server 2019 ,windows 7 , windows 10  , ubuntu Linux
-  Recommended at least 16GB RAM.
-  Oracle VM virtualbox 

## Downloading Necessary ISOs
- [PfSense](https://mirror.mahanserver.net/PfSense/2.4.5/pfSense-CE-2.4.5-RELEASE-p1-amd64.iso.gz.sha256)
- [windows server 2019](https://getintopc.com/softwares/operating-systems/windows-server-2019-standard-may-2022-free-download/)
- [ubuntu](https://ubuntu.com/download/desktop/thank-you?version=22.04&architecture=amd64)
-  [windows 7](https://getintopc.com/softwares/operating-systems/windows-7-may-2022-free-download-1792221/) 
-  [windows 10](https://getintopc.com/softwares/operating-systems/windows-10-pro-may-2022-free-download-1433484/) 
