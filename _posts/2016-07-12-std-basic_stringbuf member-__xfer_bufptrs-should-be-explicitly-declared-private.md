---
layout: post
title: std::basic_stringbuf member __xfer_bufptrs should be explicitly declared private
date: 2016-07-12 12:09
author: mazong1123
comments: true
categories: [Uncategorized]
published: true
---
In a recent project, we have to do a trick to test our legacy code. We define private keyword to public as following:

```cpp
#define private public
```

However, it does not compile under gcc 5.2.0. The compiler complains:

> std::basic_stringbuf member __xfer_bufptrs should be explicitly declared private.

After spending a lot of time by searching on the internet, we finally found this link:
https://gcc.gnu.org/bugzilla/show_bug.cgi?id=65899

> Then I suggest using -include sstream, so that stringstream is included before some idiot comes along and redefines a keyword.

Add *-include sstream* as a compile option and compile the source code again. It works like a charm. Cheers!
