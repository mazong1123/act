---
layout: post
title: Enable telnet on Windows 10
date: 2015-11-9 11:30
author: mazong1123
comments: true
categories: [Uncategorized]
published: true
---

1. In the search box enter **cmd**.
2. Right click the **Command Prompt** app and select "Run as administrator".
3. In the command prompt, execute following command:

    dism /online /Enable-Feature /FeatureName:TelnetClient
    
That's it.
