---
layout: post
title: "FarCry Poll Plugin"
date: 2011-06-14 11:20:00 -0400
comments: true
published: true
categories: [ColdFusion, FarCry]
---

I have released a plugin I have had for a while.  I'm not sure why I never got around to releasing it.  Its a very simple FarCry plugin that gives you the ability to create a one question poll and display it on the site.  It uses a couple content types and a rule.
To install, copy the files to `/farcry/plugins/spcPoll` and add `spcPoll` to your `this.plugins` setting in your FarCry constructor.  Deploy the content types in the COAPI manager and restart the application.  You can now create a question, assign answers to it, and deploy that question using the "Poll: Display Poll" rule.
You can grab the code on [Binpress](http://www.binpress.com/app/farcry-polls-plugin/474) or [Github](https://github.com/seancoyne/FarCry-Polling-Plugin).  Its also attached to this entry via the download link below.
Let me know what you think!