---
layout: post
title: Windows 10 - use ctrl+space to change input method.
date: 2015-10-17 14:19
author: mazong1123
comments: true
categories: [Uncategorized]
published: true
---
If you're using multiple input methods, you'll notice that windows 10 only supports win + space to change input methods. It's really
a pain for those who upgraded from windows 7. Fortunately, we have a simple way to save ctrl+space back in windows 10.

##Mapping ctrl+space to win+space
1. Dowanlod and install [AutoHotKey](http://www.autohotkey.com/).
2. Open notepad, copy and paste following content:

^Space::#Space

3. Save the file to any location as "inputmethod.ahk".
4. Right click "inputmethod.ahk", choose "Create a shortcut".
5. Copy "win10ChineseInutMethodFix.ahk - Shortcut" to "C:\Users\yourname\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup".
Note: change "yourname" to your account name.
6. Restart.

Now ctrl+space mapped to win+space. Happy typing! :)
