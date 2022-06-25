---
layout: post
title:  "Introduction To Linux"
date:   2021-01-05 17:06:25
categories: linux
---

## Introduction

Linux is a family of free and open-source operating systems based on the Linux kernel. Operating systems based on Linux are known as _Linux distributions_ or _distros_. Examples include Debian, Ubuntu, Fedora, CentOS, Gentoo, kali Linux, and many others.

The Linux kernel has been under active development since 1991, and has proven to be extremely versatile and adaptable. You can find computers that run Linux in a wide variety of contexts all over the world, from web servers to cell phones. Today, 90% of all cloud infrastructure and 74% of the world’s smartphones are powered by Linux.

However, newcomers to Linux may find it somewhat difficult to approach, as Linux filesystems have a different structure than those found on Windows or MacOS. Additionally, Linux-based operating systems depend heavily on working with the command line interface, while most personal computers rely on graphical interfaces.

## Why use Linux?  
- Low cost and very stable (some Linux servers are not rebooted for over a year, try that with Windows server!)  
- Best computing power and inbuilt network support.  
- Fastest developing OS,with the most number of developers.  
- Most secure OS.  
- Configurability  
- freedom

## Linux Filesystem
The **/** in the instruction above refers to the _root_ directory. The root directory is the one from which all other directories branch off from. When you run **tree** and tell it to start with _/_, you will see the whole directory tree, all directories and all the subdirectories in the whole system, with all their files, fly by.

<img src="/assets/photo/filesys.png" alt="drawing" width="660"/>


### Directories
From top to bottom, the directories you are seeing are as follows.

- **/ (root filesystem)**
The root filesystem is the top-level directory of the filesystem. It must contain all of the files required to boot the Linux system before other filesystems are mounted. It must include all of the required executables and libraries required to boot the remaining filesystems. After the system is booted, all other filesystems are mounted on standard, well-defined mount points as subdirectories of the root filesystem.

- **/bin**
/bin is the directory that contains binaries, that is, some of the applications and programs you can run. You will find the _ls_ program mentioned above in this directory, as well as other basic tools for making and removing files and directories, moving them around, and so on.

- **/boot**
/boot directory contains files required for starting your system. **DO NOT TOUCH!**. If you mess up one of the files in here, you may not be able to run your Linux and it is a pain to repair

- **/dev**
/dev contains device files. Many of these are generated at boot time or even on the fly. For example, if you plug in a new webcam or a USB pendrive into your machine, a new device entry will automagically pop up here.

- **/etc**
/etc is the directory where names start to get confusing. /etc gets its name from the earliest Unixes and it was literally “et cetera” because it was the dumping ground for system files administrators were not sure where else to put.

- **/home**
/home is where you will find your users’ personal directories. In my case, under /home there are two directories: /home/kali, which contains all my stuff; and /home/guest, in case anybody needs to borrow my computer.

- **/lib**
Contains shared library files that are required to boot the system.

- **/media**
A place to mount external removable media devices such as USB thumb drives that may be connected to the host.

- **/mnt**
A temporary mountpoint for regular filesystems (as in not removable media) that can be used while the administrator is repairing or working on a filesystem.

- **/opt**
Optional files such as vendor supplied application programs should be located here.

- **/root**
This is not the root (/) filesystem. It is the home directory for the root user.

- **/sbin**
System binary files. These are executables used for system administration.

- **/tmp**
Temporary directory. Used by the operating system and many programs to store temporary files. Users may also store files here temporarily. Note that files stored here may be deleted at any time without prior notice.

- **/usr**
These are shareable, read-only files, including executable binaries and libraries, man files, and other types of documentation.

- **/var**
Variable data files are stored here. This can include things like log files, MySQL, and other database files, web server data files, email inboxes, and much more.
