---
title: "Joining Our Machines to  the Domain And Check Machines "
layout: post
category: Active-Directory
tags: [AD, Windows-server]
excerpt: " "
---
 **join AD done under two condition**
-  DNS setting point to domin IP
-  administrator credential

# Joining a Windows 10  to the Domain

## **setting up DNS**
- search **ethernet** -> change adapter options

![Desktop View](/assets/img/AD_Lab/1 (44).png){: }

- Right-click on ethernet -> **properties**

![Desktop View](/assets/img/AD_Lab/1 (45).png){: }

- click on IPv4 -> add domin ip and router ip at DNS

![Desktop View](/assets/img/AD_Lab/1 (46).png){: }

-  check if can ping domin now  -> now can see **Domain**

![Desktop View](/assets/img/AD_Lab/1 (47).png){: }

## **join batman user to DC**
lastly, All we have left to do is join the workstation to our Active Directory domain. You used to just be able to go to system in the control panel to join the pc to the domain However Microsoft are slowly getting rid of the control panel icons and you now need to go to **Start -> Settings -> System -> About** or just search for system it will take you to the same window.

-   In the About window, click Rename this PC (advanced) in the far right menu. If initially, you can’t see the menu. Make sure to maximise the about window for the options to become avalible.

![Desktop View](/assets/img/AD_Lab/1 (48).png){: }

-   The System Properties window should appear. Click Change.

![Desktop View](/assets/img/AD_Lab/1 (49).png){: }

-   Rename the Computer From its default name. Change the member of to Domain: Then enter the name of the Active Directory Domain you created earlyer in this tutorial. If you have been following along with my examples this will be empire.local.

![Desktop View](/assets/img/AD_Lab/1 (50).png){: }

-   You will then be asked to enter a username and password. Enter the administrator details you created for your domain.

![Desktop View](/assets/img/AD_Lab/1 (51).png){: }

-   After a couple of seconds you should get a message welcoming you to the domain. Click Ok

![Desktop View](/assets/img/AD_Lab/1 (52).png){: }

-   The messages changes telling you the Computer needs to restart . Click Ok

![Desktop View](/assets/img/AD_Lab/1 (53).png){: }

- login as batman user and done 

![Desktop View](/assets/img/AD_Lab/1 (54).png){: }

#  Joining a ubuntu  to the Domain

## **setting up DNS**
-  edit resolve.conf file -> **gedit /etc/resolve.conf** -> add domain ip


![Desktop View](/assets/img/AD_Lab/1 (55).png){: }

- Install the following packages:

```bash
sudo apt install sssd-ad sssd-tools realmd adcli
```

-  Join the domain
We will use the `realm` command, from the `realmd` package, to join the domain and create the sssd configuration.
Let’s verify the domain is discoverable via DNS:

```bash
sudo realm -v discover homelab.local
```

![Desktop View](/assets/img/AD_Lab/1 (58).png){: }

## **join Flash user to DC**
- Now let’s join the domain -> add admin credential 

```bash
sudo realm join -U Administrator Homellab.local
```

![Desktop View](/assets/img/AD_Lab/1 (59).png){: }

-  Login as flash user -> done


```bash
sudo login
-> flash@homelab.local
-> password
```

![Desktop View](/assets/img/AD_Lab/1 (60).png){: }

# Check Machines on AD

![Desktop View](/assets/img/AD_Lab/1 (61).png){: }



# reference 
- https://computingforgeeks.com/join-ubuntu-debian-to-active-directory-ad-domain/ 
