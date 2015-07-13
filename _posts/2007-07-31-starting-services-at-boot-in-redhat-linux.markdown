---
layout: post
title: Starting services at boot in Redhat Linux
tags:
- linux
---
This is how to set a program (or daemon) to run at boot.  For example, if you want to run at cron at boot (which you would) issue the following as `root`.

```
/sbin/chkconfig --add crond
/sbin/chkconfig --level 2345 crond on
```

You can then confirm that it has worked by looking at `/etc/rc.d/rc2.d/S90crond`.
