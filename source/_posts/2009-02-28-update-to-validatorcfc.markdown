---
layout: post
title: "Update to ValidatorCFC"
date: 2009-02-28 09:53:00 -0400
comments: true
published: true
categories: [ColdFusion, ValidatorCFC]
---

I released a new version of ValidatorCFC.  Aaron Greenlee ([http://www.aarongreenlee.com](http://www.aarongreenlee.com)) sent me some changes.  With his changes, you can now specify which properties you want validated.  So even if in your object you say that last name and first name are required, if you pass in only the last name property, only that field will be validated.  There is more info within the CFC itself, and in the test files in the zip.  You can download the zip file using the download link on this entry, or from [RIAForge](http://validatorcfc.riaforge.org/).