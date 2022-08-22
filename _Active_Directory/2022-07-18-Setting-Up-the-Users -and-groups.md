---
title: "Setting Up the Users and Add User to groups "
layout: post
category: Active-Directory
tags: [AD, Windows-server]
excerpt: " "
---

# Setting Up the User  and groups

```console
| username  | groups | password | description |
| -------- | ------ | --------- | -------- |
| superman  | admin  | Password123!  |   |
| flash | admin | Password1!!| |
| batman  | user | Pass123456 | |
| sql server | user | Password1!!| password =>  Password1!!|
|ubuntu | user | Pass123!| Pass123!|
```

## Create user 
-  Choose Start → Windows Administrative **Tools** → **Active Directory Users and Computers.**

![Desktop View](/assets/img/AD_Lab/1 (34).png){: }


-  Right-click the Users Organizational Unit for the domain that you want to add the user to and then choose New →User from the context menu.

![Desktop View](/assets/img/AD_Lab/1 (40).png){: }

- Enter the user **logon name**. -> This name must be unique within the domain. (Don’t worry, if you try to use a name that isn’t unique, you’ll get an error message.) and Click Next.

![Desktop View](/assets/img/AD_Lab/1 (41).png){: }

-  Enter the password twice. -> You’re asked to enter the password and then confirm it, so type it correctly. If you don’t enter it identically in both boxes, you’re asked to correct your mistake.

![Desktop View](/assets/img/AD_Lab/1 (37).png){: }

- Verify that the information is correct and then click Finish to create the account.

![Desktop View](/assets/img/AD_Lab/1 (38).png){: }

## Add User To Group
- add superman user to admin group -> first Right-click on the name of user and click 
**properties**->  and click on **member of**  -> click on **Add** -> add group name that you want add user to  ex. add **superman** to  **Administrators** group -> click **ok** 

![Desktop View](/assets/img/AD_Lab/1 (42).png){: }

- verify it ->  Right-click on the name superman of user and click  **properties**

![Desktop View](/assets/img/AD_Lab/1 (43).png){: }



