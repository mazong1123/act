---
layout: post
title: Add another java project as dependency in eclipse
date: 2015-12-26 21:01
author: mazong1123
comments: true
categories: [Uncategorized]
published: true
---

Let's say we have 2 projects A and B. Project A is the dependency of project B.

1. Right click project B -> **Build Path** -> **Configure Build Path**. In the popup dialog, select **Projects** tab, and add project A.

2. Right click project B -> **Properties**. In the popup dialog, select **Deployment Assembly** in the left side bar, and add project A.

Done. Happy coding!
