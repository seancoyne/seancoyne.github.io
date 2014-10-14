---
layout: post
title: "FarCry LESS Plugin"
date: 2012-04-10 11:26:00 -0400
comments: true
published: true
categories: [ColdFusion, FarCry]
---

Today I released a [plugin for FarCry](https://github.com/seancoyne/farcryless) that will automatically compile your [LESS](http://lesscss.org/) files into CSS. No more need to compile on your development machine before you push to production, and no more need to punish your users by compiling on the client side with [Less.js](https://github.com/cloudhead/less.js). While those solutions are perfectly acceptable, this plugin will let you simply code in LESS, then let FarCry do the work of serving compiled, minified CSS to your users.
The plugin uses a similar syntax to FarCry's built in skin:loadCSS tag so it should be instantly familiar.  Be sure to read the installation instructions to avoid a couple of potential "gotchas".
[Check it out on Github](https://github.com/seancoyne/farcryless), and let me know if its useful for you, or if you would like to see any additional features.