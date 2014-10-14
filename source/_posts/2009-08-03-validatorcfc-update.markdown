---
layout: post
title: "ValidatorCFC Update"
date: 2009-08-03 11:56:00 -0400
comments: true
published: true
categories: [ColdFusion, ValidatorCFC]
---

Just a 
quick note, thanks again to [Aaron Greenlee](http://www.aarongreenlee.com/) I have some 
small modifications to [ValidatorCFC](http://validatorcfc.riaforge.org/).

The 
modifications allow you to return a struct where the key is the name of 
the field in your object, and the value is true/false indicating if it 
passed validation.

This is useful if you prefer more control when 
showing informative messages to the user.

The zip file is 
attached to this entry as well as at [RIAForge](http://validatorcfc.riaforge.org/).