---
layout: post
title: "ColdFusion 9 and mod_jrun on Mac OS X Yosemite with Apache 2.4"
date: 2014-10-13 19:30:00 -0400
comments: true
published: true
categories: [ColdFusion, Apache]
---

OS X Yosemite updates the included Apache HTTP server from 2.2 to 2.4. The ColdFusion 9 connector installs a version of mod_jrun which has been compiled for Apache 2.2. Using [this article](https://research.g0blin.co.uk/mod_jrun-on-apache-2-4-ubuntu-14-04-coldfusion-9/) I was able to recompile the connector for Apache 2.4 and get ColdFusion 9 running with Apache 2.4. Attached to this you will find a zipped version of the connector so you can skip recompiling it yourself. Simply unzip and move the .so file to the desired location on your Mac and update your Apache configuration to point to it.
So:
```
LoadModule jrun_module /Applications/JRun4/lib/wsconfig/1/mod_jrun22.so
```
becomes
```
LoadModule jrun_module /Applications/JRun4/lib/wsconfig/1/mod_jrun24.so
```
You may find you need to update other Apache configuration settings. You can find additional information on upgrading from Apache 2.2 to 2.4 in the [Apache HTTP Server Documentation](http://httpd.apache.org/docs/2.4/upgrading.html).