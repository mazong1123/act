---
layout: post
title: Windows 10 - remote desktop to CentOS
date: 2015-11-9 10:53
author: mazong1123
comments: true
categories: [Uncategorized]
published: true
---

Recently, I have a project needs to be developed on CentOS with C/C++. I decided to setup a CentOS VM and remote from my Windows 10 PC.
To enable the RDP from windows to linux, I've found a very useful article [HERE](http://broexperts.com/2014/07/how-to-remote-desktop-linux-machine-from-windows-7/).
However, there's a missing step and some typos in the article. So I decide to re-write the article as following:

##Step 1: Find OS Architecture
First, su as root:

  [xxx@BroeExpertsSRV~] $ su

Enter following command to find the OS architecture.

  [root@BroeExpertsSRV~] # uname -r

If the output shows x86_64 at end then mean, you have a 64-bit install or if it shows i386 then your OS architecture is 32-bit.
Our output is showing (2.6.32-279.el6.i686) it’s mean we have 32-bit operating system.
After determining your architecture, install the correct EPEL repository with below command.

##Step 2: Download And Install The Correct EPEL Repository
For RedHat or Centos 6.x 32-bit

  [root@BroeExpertsSRV~] # wget http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
  [root@BroeExpertsSRV~] # rpm -ivh epel-release-6-8.noarch.rpm

For RedHat or Centos 6.x 64-bit

  [root@BroeExpertsSRV~] # wget http://download.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
  [root@BroeExpertsSRV~] # rpm -ivh epel-release-6-8.noarch.rpm

##Step 3: Verify EPEL Repository Is Installed Correctly

  [root@BroeExpertsSRV~] # yum repolist -v | grep epel

We can see EPEL repository is installed correctly.

##Step 4: Install XRDP Package.
Now we are ready to install XRDP package. It will install also some dependencies.

  [root@BroeExpertsSRV~] # yum install xrdp tigervnc-server

##Step 5: Config VNCServers
After instllation we need to configure display.
Edit display file located at /etc/sysconfig/vncservers

  [root@BroeExpertsSRV~] #vim /etc/sysconfig/vncservers

**Find at last these lines**

  # VNCSERVERS="2:myusername"
  # VNCSERVERARGS[2]="-geometry 800×600 -nolisten tcp -localhost"

Uncomment and change them into:

  VNCSERVERS="2:root"
  VNCSERVERARGS[2]="-geometry 1024×768"

I am using root user as my remote desktop user.
Now save this file and exit.

##Step 6: Set VNCServer Password
Enter following command to set VNCServer for current user.

  [root@BroeExpertsSRV~] # vncserver

You will be prompted for entering new password for the current vncserver user.

##Step 7: Start VNC And XRDP Services

  [root@BroeExpertsSRV~] # service vncserver start
  [root@BroeExpertsSRV~] # service xrdp start

##Step 8: Make VNC And XRDP Services Available On Startup

  [root@BroeExpertsSRV~] # chkconfig xrdp on
  [root@BroeExpertsSRV~] # chkconfig vncserver on

##Step 9: Allow 3389 Port In iptables

  [root@BroeExpertsSRV~] # iptables -I INPUT -p tcp --dport 3389 -j ACCEPT
  [root@BroeExpertsSRV~] # service iptables save
  [root@BroeExpertsSRV~] # service iptables restart

##Step 10: Connect to Linux from Windows
Start **Remote Desktop Connection** on Windows, enter the ip address of your Linux box, enter user name and password. That's it.
