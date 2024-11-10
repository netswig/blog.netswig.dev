---
date:
  created: 2024-11-10
categories:
    - Cisco IOS
tags: 
- Cisco IOS
draft: false
---

# Cisco IOS - Working With Text Files

## The Problem
Generally when working with a Cisco device's text configuration files, the files are copied to the device using methods like SCP,FTP or TFTP. 

However many times I have found myself in a situation where I do not have a server available to me to copy files to/from. 

Its also common I cannot create a server due to security restraints or having no available compute resources.

Below are some useful tricks to get around this problem.

<!-- more -->

## Reading Files

The `more` command can be used to output the contents of a text file to the console. This is useful for reading any files already stored on a devices flash. 

### Example

```cisco title="Using the 'more' command"
hq-ios-nr-01#more flash:config-backup.ios           
!
! Last configuration change at 18:59:28 UTC Sun Nov 10 2024
!
version 15.6
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname hq-ios-nr-01
!
boot-start-marker
boot-end-marker
!
!
.....
```

```cisco title="Using the 'more' command with section output modifiers"
hq-ios-nr-01#more flash:config-backup.ios | s line 
line con 0
line aux 0
line vty 0 4
 privilege level 15
 login local
 transport input ssh
```

## Creating Files

For devices which do not have any container or linux guest shell capabilities you can use the TCL shell to create files.

### Example

```cisco title="Creating new config file using TCL Shell"
hq-ios-nr-01(tcl)#puts [open "flash:config-new.ios" w+] {
+>version 15.6
+>service timestamps debug datetime msec
+>service timestamps log datetime msec
+>service password-encryption
+>!
+>hostname hq-ios-nr-01-new
+>!
+>boot-start-marker
+>boot-end-marker
.....
+>}
hq-ios-nr-01(tcl)#tclquit
```