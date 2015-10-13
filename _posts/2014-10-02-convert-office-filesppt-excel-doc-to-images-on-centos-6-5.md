---
layout: post
title: Convert office files(ppt, excel, doc...) to images on CentOS 6.5
date: 2014-10-02 10:09
author: mazong1123
comments: true
categories: [centos, convert, doc, excel, image, imagemagick, linux, pdf, ppt, unoconv]
---
There's a requirement in my recent project to convert office files to multiple images. After hard work for a week, I found the correct steps that cannot be searched through Google. I'm going to write it down, hope these steps save your time.
<h1>Brief</h1>
Use <strong>unoconv</strong> to convert office files to PDF, then convert PDF to images leveraging <strong>ImageMagick</strong>.
<h1>Install unoconv</h1>
1. Visit http://wiki.centos.org/AdditionalResources/Repositories/RPMForge. Download RPMforge for CentOS 6 via <strong>wget</strong>. In my case, I downloaded <strong>i686 rpm</strong>.

<a href="https://mazong1123.files.wordpress.com/2014/10/1.png"><img class="alignnone size-medium wp-image-82" src="http://mazong1123.files.wordpress.com/2014/10/1.png?w=300" alt="1" width="300" height="97" /></a>

Run following command to install the rpm key:

<strong>rpm --import http://apt.sw.be/RPM-GPG-KEY.dag.txt</strong>

Run<strong> rpm -Uvh</strong> to install the downloaded rpm file.

2. Create a file Archives.repo under /etc/yum.repos.d/. Add following contents to Archives.repo :

[c6-archives]
name=CentOS-6 – Archives
baseurl=http://vault.centos.org/6.2/updates/$basearch/
gpgcheck=0
enabled=1

3. Run following comand:

<strong>yum clean all</strong>

4. Run following command:

<strong>yum install unoconv openoffice.org-headless openoffice.org-writer openoffice.org-calc openoffice.org-impress</strong>
<h1>Install ImageMagick</h1>
Run following command:

<strong>yum install ImageMagick</strong>
<h1>Install Fonts</h1>
CentOS does not support enough fonts by default (e.g Chinese fonts). Therefore the converted file may contain unexpected characters. The easiest way to resolve this issue is to copy fonts from Windows.

1. Create a folder named <strong>win</strong> in driver D of your Windows.

2. Copy all files under C:\WINDOWS\Fonts to D:\win.

3. Upload folder <strong>win</strong> to your CentOS 6.5 server(via winscp, or FTP tools).

4. Run following command in CentOS:

mv win /usr/share/fonts

cd win

mkfontscale

mkfontdir

fc-cache  -fv

5. Restart CentOS server.
<h1>Convert</h1>
Using following commands to convert an office file to images:

First convert office file to pdf:

'unoconv -f pdf resume.ppt'

Convert pdf to images:

mkdir resume

'convert resume.pdf resume/resume_%03d.jpg'

I've written a nodeJS wrapper:

var sys = require('sys');

var exec = require('child_process').exec;

console.log('converting to pdf...');

exec('unoconv -f pdf resume.ppt', function(error, stdout, stderr){

console.log('converted resume.pdf');

console.log('converting resume.pdf to multiple pics...');

exec('convert resume.pdf resume/resume_%03d.jpg', function (error, stdout, stderr){

console.log('All done');

});

});

That's all. Cheers!
