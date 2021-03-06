---
layout: post
title: How to configure cache-control in Tomcat
tags:
- java
- tomcat
---
I ran into a major problem with IE (**shudder**) not being able to open files. I could save them fine, but when I went open, the application would complain that it couldn’t find the file. I found that the problem was not the java application but the webserver itself. Using a very useful tool called [Fiddler](http://www.fiddlertool.com) I looked at the HTTP request headers and found that the webserver was overwriting the headers I set in Java.

I found that the headers were:

```
HTTP/1.1 200  OK
Server:  Apache-Coyote/1.1
Date: Mon, 09 Jul 2007  22:50:18 GMT
Content-type:  application/octet-stream
X-powered-by:  Servlet/2.4
Pragma:  No-cache
Cache-control:  no-cache
Expires: Thu, 01 Jan  1970 12:00:00 NZST
Content-disposition:  attachment; filename=trace-64.pcap
Transfer-encoding:  chunked
```

Setting `no-cache` means that IE downloads the file, but then it expires it in cache, it gets deleted and hence the application cannot open the file. After much searching around the internet, I found [a post which describes how to do it](http://www.symphonious.net/2007/06/19/caching-in-tomcat/trackback/).

I added the below to my `META-INF/context.xml`:

```
<Valve className="org.apache.catalina.authenticator.BasicAuthenticator" disableProxyCaching="false" />
```

Once Tomcat is restarted, the headers are now:

```
HTTP/1.1 200  OK
Server:  Apache-Coyote/1.1
Content-Disposition:  attachment; filename=filename.txt
Content-Type:  application/octet-stream
Transfer-Encoding:  chunked
Date: Mon, 09 Jul 2007  22:59:01 GMT
```

IE now can open files!!!!! Credit goes to above post ;)

This works for me when included in the `.war` file, and it now works in Firefox **and** IE.
