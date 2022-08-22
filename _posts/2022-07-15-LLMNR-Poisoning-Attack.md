---
title:  LLMNR & NBT-NS Poisoning  Attack 
layout: post
category: Active-Directory
tags: [LLMNR, hashcat ]
excerpt: " "
---

# LLMNR  & NBT-NS Poisoning Overview
LLMNR stand for **Link-Local Multicast Name Resolution**  and NetBIOS Name Service (**NBT-NS)** are two name services used by windows for resolving hostnames to IP addresses when a DNS request fails in a network.

In a network, if a machine tries to resolve a particular host and DNS fails to do so, the machine will communicate with other machines in the network using the LLMNR and ask if anyone knows the particular hosts.

In Active Directory environments, we often see that LLMNR is enabled and it is used widely. But using the LLMNR host resolution has a severe security impact, as when a non-existing host is searched using the **LLMNR** method. it broadcasts the request to every system that is connected to the local network. and if we have any compromised machine on the local network by default it will also receive the host query request and the compromised machine can also send the response to the victim machine. and in turn, ask for the password hash of the victim.

![Desktop View](/assets/img/AD_Lab/1 (63).png){: }


-   the victim machine wants to connect **\sharefiles**, but mistakenly typed in **\shrefiles**
-   The DNS server responds to the victim **_\\shrefiles_** — **NOT FOUND**
-   then the victim sends out a Broadcast asking if anyone on the local network knows the location of **_\\shrefiles_**
-   The compromised attacker machine responds to the victim, saying that it is **\\shrefiles** accepts the victim's username and NTLMv2 Hash
-   and then the responder sends an error message back to the client.

# LLMNR Poisoning Attacks 

- To begin the attack, we start an LLMNR/NBT-NS poisoner such as Responder. Responder can listen for the LLMNR/NBT-NS queries being broadcast on the local network and by default also sets up several different servers, most notably SMB. These will be used to receive authentication requests after the poisoning.

```bash
responder -I eth1 -dvw 
```

![Desktop View](/assets/img/AD_Lab/1 (64).png){: }

You can see below that while listening for events, Responder has picked up an LLMNR query and has proceeded to poison these requests.

These LLMNR queries were not for any service that could be useful to an attacker, however, if we now go to one of the lab machines and accidentally mistype a file share name (making use of the SMB protocol), the victim computer will attempt to authenticate to this spoofed share. Please see below where we have tried to look up ‘**\\sshare’** which does not exist.

![Desktop View](/assets/img/AD_Lab/1 (65).png){: }


If we now check back with Responder, we can see that the authentication negotiation has taken place and we have now captured Jo Blogg’s username and NetNTLMv2 (NTLMv2) hash.

![Desktop View](/assets/img/AD_Lab/1 (66).png){: }

NTLMv2 hashes cannot be used in a Pass-the-Hash attack (which uses standard NTLM hashes), however, the hashes can be cracked to derive the cleartext password, which can be done using a cracking tool such as hashcat or John the Ripper. If you can obtain the cleartext credentials and the domain is configured to allow remote login via protocols such as SMB (i.e. FilterAdministratorToken is not set to 0 in the registry), you may be able to login to other hosts on the network. Please note that remote login is only possible where the victim user is a local administrator on the target machine.

#  crack hashes  

> hashcat -m 5600 hashes.txt rockyou.txt  
- 5600 is modal called 'netntlmv1' network protocol  
- used help hashcat --help
- rockyou is wordlist can download it seclist github



# LLMNR Poisoning  Mitigation
The simplest way to defend against LLMNR/NBT-NS poisoning is to disable both LLMNR and NBT-NS completely. For networks that use an ordinary DNS server for name resolution, disabling LLMNR and NBT-NS should have no adverse effects, and by disabling these services you will have closed a prominent security hole.

## DISABLE LLMNR
1.  Open ‘Group Policy Management’ on the domain controller.
2.  Add a new GPO (Forest -> Domains -> Your Domain -> Group Policy Objects and Right Click -> New)
3.  You can name the new GPO whatever you like but we’ve called it ‘LLMNR Disabled’.
4.  Right Click the new GPO and select ‘edit’.
5.  Go to Computer Configuration -> Policies -> Administrative Templates -> Network -> DNS Client
6.  Double click ‘Turn off multicast name resolution’ and select ‘Enabled’.
7.  Click ‘Apply’ and then ‘OK’

## DISABLE NBT-NS
1.  Go to Control Panel -> Network and Internet -> Network and Sharing Centre -> Change Adapter Settings
2.  Right click the network interface in use and choose ‘Properties’.
3.  Double click ‘Internet Protocol Version 4 (TCP/IPv4)’ and then click ‘Advanced’
4.  Go to the ‘WINS’ tab, click ‘Disable NetBIOS over TCP/IP’ and then click ‘OK’.



# reference
- https://systemweakness.com/what-is-llmnr-poisoning-attack-and-how-to-secure-against-it-417f3b415e51
- https://www.cynet.com/attack-techniques-hands-on/llmnr-nbt-ns-poisoning-and-credential-access-using-responder/

