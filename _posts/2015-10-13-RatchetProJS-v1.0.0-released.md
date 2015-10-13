---
layout: post
title: RatchetProJS v1.0.0 released! A lightweight mobile framework let you build things easier.
date: 2015-10-13 14:19
author: mazong1123
comments: true
categories: [Uncategorized]
published: true
---

So what's [RatchetPro.js](https://github.com/mazong1123/ratchet-pro)? Two years ago, I found a prime project released by twitter - [Ratchet.js](https://github.com/twbs/ratchet). It's lightweight, only contains core functions to run HTML5 web apps. Compare to JQuery Mobile or Sencha Touch, it's more like a library other than a framework. It's extremely useful if you already familiar with bootstrap. I implemented my several mobile HTML5 apps based on Ratchet.js and it runs very smoothly and quickly.

However, [Ratchet.js has stopped updating for over a year](https://github.com/twbs/ratchet/issues/792). It's sad. As small and lightweight library is more and more poplular than a big, full-featured framework nowadays, Ratchet.js should be a perfect solution to provide basic infrastructure of a web app. Hence, I decided to fork Ratchet.js and continue the development of it. That's why RatchetPro.js coming out.

The main improvement of the RatchetPro.js v1.0.0 is introduced PageManager. It solves the problem of ["Execute custom script after page loaded with Ratchet\Push.js"](http://stackoverflow.com/a/33099026/2719128) and ["Executing several JS files with Ratchet push.js library"](http://stackoverflow.com/a/33005426/2719128). It also takes care of caching loaded js.

The documentation and examples can be found [HERE](https://github.com/mazong1123/ratchet-pro). Happy coding :)
