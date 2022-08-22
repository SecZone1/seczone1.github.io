---
title: "Setting Up the PFSense and Active Directory "
layout: post
category: Active-Directory
tags: [AD, Windows-server]
excerpt: " "
---


# Setting Up Domain Controller
In this part of the tutorial, we are going to be setting up Domain Controller on our new Windows 2019 server. Domain Controller is a directory service that runs on Microsoft Windows Server that allows administrators to manage permissions and control access to network resources. Within Active Directory data is stored as objects, which include users, groups, applications, and devices.

So let’s Get started.


-   Firstly start by opening **Server Manager**. This may take a few miniutes for it to populate all the data.

![Desktop View](/assets/img/AD_Lab/1 (23).png){: }

-   Once Server Manager is open Click **Manage** and then **Add Roles and Features**.

![Desktop View](/assets/img/AD_Lab/1 (22).png){: }

-   In the Add roles and features wizard click the third option on the left menu for server selection and you will then be able to select Server Roles.

![Desktop View](/assets/img/AD_Lab/1 (24).png){: }

-   Tick the box next to Active Directory **Domain Services**.

![Desktop View](/assets/img/AD_Lab/1 (25).png){: }

-   You will then be prompted with a window showing all the services or features that will be installed. have a quick read through whats being installed. Make sure include managment tools is selected and click add feature.

![Desktop View](/assets/img/AD_Lab/1 (26).png){: }

-   Click Next to move to features. **leave everything as default**.

![Desktop View](/assets/img/AD_Lab/1 (27).png){: }

-   Now click Next through AD DS, DHCP Server and DNS Server leaving everything as default until you get to confirmation. From here click **Install**

![Desktop View](/assets/img/AD_Lab/1 (28).png){: }

- This will  install everything needed for Active Directory Domain Services

![Desktop View](/assets/img/AD_Lab/1 (29).png){: }

-   In Server manager you should now see the Flag has a yellow triangle next to it. click this and **select Promote this Server to a domain controller**.

![Desktop View](/assets/img/AD_Lab/1 (30).png){: }

-   You should see the Active Directory Domain Services Configuration Wizard pop up. Select Add a **new forest** and enter a domain name.  -> **Homelab.local**

![Desktop View](/assets/img/AD_Lab/1 (31).png){: }

-   In the Domain Controller Options, set an Directory Services Restore Mode password, confirm the password and then click next.

![Desktop View](/assets/img/AD_Lab/1 (32).png){: }

- Click Next , Click Next , -   The Server will run through some Prerequisites checks. Dont worry to much about the errors generated here and click install.

![Desktop View](/assets/img/AD_Lab/1 (33).png){: }

Once the Server has finished being promoted to a domain controller, Reboot to complete the Installation.


