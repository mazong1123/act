---
layout: post
title: How to invoke InfoPath designer within SharePoint list data.
date: 2010-10-22 15:57
author: mazong1123
comments: true
categories: [Uncategorized]
---
SharePoint 2010 has a new feature that can "Customize List" with InfoPath 2010. So how can the system do it? Just one command line can tell you the truth:

infopath.exe /spSiteURL <a href="http://server%22/" target="_blank">http://sitename</a> /spListID "{524E9C94-639F-4F95-8AD7-C699CBA499BF}" /design /noautoformsdialog

OK. Now specify your site name and list ID, you have the same functionality of "Customize List" ribbon button. /spSiteURL and /spListID are unreleased parameters. Have fun!
