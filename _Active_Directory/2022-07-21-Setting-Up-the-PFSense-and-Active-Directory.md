---
title: "Setting Up the PFSense and Active Directory "
layout: post
category: Active-Directory
tags: [AD, Windows-server]
excerpt: " "
---

# Setting Up the PFSense 
-  Firstly start by creating a New virtual Machine. Give the New Virtual machine a Name and point to where you want to store the VMs. Select the type as BSD and the OpenBSD \\64 Bit Version.

![Desktop View](/assets/img/AD_Lab/1 (3).png){: }

 - Set the amount of memory you want to allocate to the PFsense firewall. I have used the **Minimum of 512MB** on this tutorial which should be fine for this lab. However, if you find this a bit slow you can always throw extra memory at it in the future.

![Desktop View](/assets/img/AD_Lab/1 (5).png){: }

- On the Hard Disk selection, select that you want to create the Virtual hard disk now and click the Create button.
- You should now be in the Create Virtual Hard Disk window. Check the file location where you want to store the Virtual Machines is correct. Keeping with the Minimum requirements, set the **Virtual Machine file Size to be at least 8GBs**. Leave everything else default.

![Desktop View](/assets/img/AD_Lab/1 (6).png){: }

- Go to the settings of the new Pfsense Virtual machine and select storage and insert the pfsense CD you downloaded at the [first tutorial](https://seczone1.github.io/Active_Directory/2022-08-01-Introduction-And-Scenario).

![Desktop View](/assets/img/AD_Lab/1 (7).png){: }

- Staying in Settings of the PfSense Virtual Machine, select the Network tab. **The first adapter needs to be setup as a bridged adapter**, also select which of the host’s physical network adapters to use. ->  **WAN** 

![Desktop View](/assets/img/AD_Lab/1 (8).png){: }

- Then **Select the Adapter 2 tab** and select the tick box to enable the 2nd network adapter.
- Set Attached to **Internal Network** and type a name for your internal network. I use name **LAB** but you can call it anything you like. -> **LAN**

![Desktop View](/assets/img/AD_Lab/1 (9).png){: }

- Click Ok to save the configuration, Then start then PFSense Virtual Machine. This should run the PFSense ISO we added earlyer. After a few minutes, you should see the PFSense installer message below.

![Desktop View](/assets/img/AD_Lab/1 (10).png){: }

-   Accept the Copyright, then select Install and OK.
-   With the arrow keys find the keyboard layout you want, then hit enter to select. 


![Desktop View](/assets/img/AD_Lab/1 (11).png){: }

-   Next is partitioning the Virtual Hard disk. Just use the **Auto (UFS)** Guided disk setup and select OK.
-   The PFSense installer should then start.

![Desktop View](/assets/img/AD_Lab/1 (12).png){: }

-   With Pfsense installed, Select **No** in regards to doing a manual configuration.
-   With PFSense now configured and installed, Select reboot. PfSense should then load.

**Note:** Make sure you dismount the PFSense CD otherwise the CD will start the installer again

![Desktop View](/assets/img/AD_Lab/1 (13).png){: }

- Once PFSense has fully rebooted you should see a screen that looks as below. The Wan address should be an IP on your home network and the LAN on a completley diffrent IP range. In my case that IP is 192.168.1.1/24.

![Desktop View](/assets/img/AD_Lab/1 (14).png){: }


# Setting Up the Active Directory 

**After install windows server 2019 **
**Remember:** if you called the internal network something other than LAN when you set up the PFSense Firewall switch it to this instead.

![Desktop View](/assets/img/AD_Lab/1 (15).png){: }

## Set a static IP Address
Open Control Panel and click view network status and task

![Desktop View](/assets/img/AD_Lab/1 (16).png){: }

-   In Network and Sharing Center click Change Adapter settings in the menu on the left.

![Desktop View](/assets/img/AD_Lab/1 (17).png){: }

-   Right click the network conection called Ethernet and select properties.

![Desktop View](/assets/img/AD_Lab/1 (19).png){: }

-   Then left click Internet Protocol Version 4 (TCP/IPv4) so its highlighted and click properties.
-   Switch both the IP address and DNS from automatically obtain too use the following and to keep things simple enter the Static IP details below.

![Desktop View](/assets/img/AD_Lab/1 (20).png){: }

When these are all set just hit OK and the New IP address settings will take effect.

## Set Server/PC Name

-   Firstly open Control Panel and select System
-   When the system window opens click the change Settings button in the Computer name, Domain and workgroup settings section.
-   Delete the Current default name of the server and replace it with **Local-DC**. You can call the server anything you want however if you want to follow along keep it as Local-DC.

![Desktop View](/assets/img/AD_Lab/1 (21).png){: }

 windows will restart , and you are read to go 














