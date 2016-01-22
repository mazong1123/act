---
layout: post
title: Setup cdt with cygwin
date: 2016-1-22 12:09
author: mazong1123
comments: true
categories: [Uncategorized]
published: true
---
To setup CDT with cygwin, following below steps.

1.Project -> Properties -> C/C++ General -> Preprocessor Include,
select CDT GCC Built-in Compiler Settings Cygwin, check "Use global provider shared between projects".

![cdt-1](images/cdt-1.png)

2.Project -> Properties -> C/C++ General -> Paths and Symbols,
select Symbols -> GNU C++, add following Symbol

```
_cplusplus
```

with value:

```
201303L
```

![cdt-2](images/cdt-2.png)

3.Project -> Properties -> C/C++ Build -> Settings, select Cygwin C++ Compiler. Change command to

```
g++ -std=c++11
```

![cdt-3](images/cdt-3.png)

4.Project -> Properties -> C/C++ Build -> Settings, select Cygwin C++ Commpiler -> Dialect, Select ISO C++11 (-std=c++0x).

![cdt-4](images/cdt-4.png)
