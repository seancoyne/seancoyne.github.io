---
layout: post
title: "Adobe releases hotfix for FCKEditor issue"
date: 2009-07-08 15:02:00 -0400
comments: true
published: true
categories: [ColdFusion]
---

Adobe has released a hotfix for the FCKeditor issue.  You can find it [here](http://www.adobe.com/support/security/bulletins/apsb09-09.html).
Take notice that it says to first stop the CF service and then access the CF 
administrator.  This is impossible.  Simple open the administrator first 
and apply the hot fix on the system info screen.
Also, Mac (linux too??) users should know that if you unzip the cfide.zip file to 
the cfide folder it will replace the folder not merge the files like on 
windows.  You will be left without a working CFIDE folder.  You should 
manually merge the files.