---
layout: post
title: "Running ColdFusion 10 on OS X Mavericks"
date: 2013-10-23 12:03:00 -0400
comments: true
published: true
categories: [ColdFusion, Apache]
---

Running ColdFusion 10 on OS X Mavericks is possible, but not straightforward.  Unfortunately, it seems the web server connector does not work with Apache 2.2.24 which ships with Mavericks.  A bug has been logged for this here: [https://bugbase.adobe.com/index.cfm?event=bug&amp;id=3653076](https://bugbase.adobe.com/index.cfm?event=bug&amp;id=3653076).  Please vote for it.
There are a couple of issues I had with Mavericks and ColdFusion 10 (CF 9 works fine for me for what it is worth).
First, ColdFusion wouldn't start because Mavericks removed Java 6.  I had to update 3 files to fix this:

`/Applications/ColdFusion10/cfusion/bin/jvm.config`
`/Applications/ColdFusion10/cfusion/bin/coldfusion`
`/Applications/ColdFusion10/cfusion/runtime/bin/wsconfig_jvm.config`
 
In each of these, there was a setting to set the Java home path.  It was set to the old location for Java 6.  I updated these to point to Java 7.  For me this was:

`/Library/Java/JavaVirtualMachines/jdk1.7.0_45.jdk/Contents/Home`

This was after installing the [latest Updater 45 JDK from Oracle's website](http://www.oracle.com/technetwork/java/javase/downloads/index.html).

Once I made these changes ColdFusion started fine.

The next issue is with the Connector.  Adobe created a customized version of mod\_jk to go along with their customized version of Tomcat.  Because of this, recompiling mod\_jk is not going to work. ~~We'll have to wait for an updated version from Adobe.~~ (**EDIT:** See Mike's comment [below](#comment-1635209099) for a solution!) Until then you can either use the built in web server or install MAMP PRO which ships with Apache 2.2.22 (same as Mountain Lion) and then configure using the web server connector.

I followed the recommendations in this blog post: [http://www.brilang.com/2012/06/installing-coldfusion-10-under-mamp-pro-2-on-os-x-lion/1137](http://www.brilang.com/2012/06/installing-coldfusion-10-under-mamp-pro-2-on-os-x-lion/1137) to configure MAMP PRO.