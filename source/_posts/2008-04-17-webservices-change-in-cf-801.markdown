---
layout: post
title: "Webservices Change in CF 8.0.1"
date: 2008-04-17 04:50:00 -0400
comments: true
published: true
categories: [ColdFusion, Web Development]
---

It seems with the change to 8.0.1 there is a difference in the 
way CF generates the stubs for a CFC called as a web service.  I had a 
CFC called webservices.cfc and on 8.0 it was working fine calling the 
methods, but with the 8.0.1 it started throwing a "duplicate file name" 
error.  This seems to be because CF creates its own stub file 
`Webservices.java` and also a `[cfcname].java` file.  CF couldn't create 
both so it threw an error.  The solution was to rename my CFC.  The 
stubs can be found in `C:\ColdFusion8\stubs\` on Windows, and if I 
remember correctly `/Applications/ColdFusion8/stubs/` on Mac OS X.