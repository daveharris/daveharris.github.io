---
layout: post
title: "Show current and upgraded package versions in Yum"
date: 2014-08-04 14:37
comments: true
categories: 
status: publish
published: true
categories:
- ! '*nix'
- How-to
---

Have you ever wanted to know the list of packages which are about to be installed, including the current version and what version it is going to be updated to? Well, I have the solution:

```bash
yum list updates 2>&1 | grep x86_64 | while read line; do PACKAGE=`echo $line | awk '{print $1}'`; VERSION=`echo $line | awk '{print $2}'`; echo "$PACKAGE - `rpm -q $PACKAGE --qf '%{VERSION}-%{RELEASE}\n'` --> $VERSION"; done
```

It seems like `yum list` should provide this option.