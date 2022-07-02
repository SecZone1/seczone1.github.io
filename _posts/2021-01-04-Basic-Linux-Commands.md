---
layout: post
date:   2021-01-05 17:06:25
categories: [linux, PT]
---

## FILE COMMANDS


- Is   =   directory listing   
- Is -al   =    formatted listing with hidden files   
- cd dir     =    change directory to dir   
- pwd    =   show current directory   
- mkdir dir    =     create directory dir   
- rm file     =    delete file   
- rm -r dir     =     delete directory dir   
- rm -f file     =     force remove file  
- rm -rf dir     =     force remove directory  
- cp filel file2     =     copy filel to file2  
- mv filel file2     =     rename filel to file2   
- In -s file link     =     create symbolic link 'link' to file       
- touch file      =  create or update file      
- cat > file      =  place standard input into file     
- more file      =  output the contents of the file   
- less file      =  output the contents of the file   
- head file      = output first 10 lines of file   
- tail file      =  output last 10 lines of file   
- Mail -f file      =  output contents of file as it grows 


## NETWORK COMMANDS


- ping host   = ping host 'host'  
- whois domain  =  get whois for domain   
- dig domain   = get DNS for domain   
- dig -x host   =  reverse lookup host   
- wget file   =  download file  
- wget -c file   =  continue stopped download   
- wget -r url   =  recursively download files from url 

## ssh COMMANDS


- ssh user@host    =   connect to host      
- ssh -p port user@host    =   connect using port p     
- ssh -D port user@host    =  connect & use bind port     


## SYSTEM INFO


- date    |   show current date/time   |  
- cal    =   show this month’s calendar     
- uptime    =   show uptime     
-  w    =   display who is online   
- whoami    =   who are you logged in as     
-  uname -a    =   show kernel config   
- cat /proc/cpuinfo    =   cpu info       
- cat /proc/meminfo    =   memory info     
- man command   =   show manual for command     
- df    =   show disk usage     
- du   =   show directory space usage   
- du-sh   =   human readable sizein GB     
- free    =  show memory & swap usage     
- which app   =  show which app will be run by defaul   

## PROCESS MANAGEMENT


-  ps     =    display :currently active processes 
-  ps aux     =   ps with a lot of detail    
-   kill pid     =     kill  process  pid 'pid'    
-  bg     =    lists stopped/background jobs    
- fg     =    bring most recent job to foreground      
- fg n     =   brings job n to foreground     



## FILE PERMISSIONS

-  chmod octal file      =    change  permission of file (4:read / 2:write / 1:execute) Order : owner/group/world      
-  Eg:chmod755file     =    readwritefor owner, read execute for group/world     



## COMPRESSION

- tar **cf** file.tar files     =     tar files intoi file.tar        
- tar **xf** file.tar    =     untar into current directory  
- tar **tf** file.tar   =   show contents of archive     


## SEARCHING

- grep pattern files     =      search for pattern in files     
- command |   grep pattern      =       search for pattern in output of the command         
- locate file     =      search for files in all file system         
