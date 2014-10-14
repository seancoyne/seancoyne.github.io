---
layout: post
title: "FarCry Slider Formtool"
date: 2011-09-20 21:37:00 -0400
comments: true
published: true
categories: [ColdFusion, FarCry]
---

I posted this on the [farcry-dev](https://groups.google.com/group/farcry-dev) mailing list but thought I would post it here as well to help future googlers in need.

I have created a slider formtool for a client and thought it could be useful to others in the community. You can find the source for it here: [https://gist.github.com/1230366](https://gist.github.com/1230366)

<!-- more -->

{% gist 1230366 %}

To use, simply download the CFC, and place it in your project's `/farcry/projects/projectname/packages/formtools` directory. Once there, you specify the metadata in your custom types as you would use any other formtool.

{% gist 8810243 %}

The formtool is an extension of the numeric formtool found in core, so you can use any of the features found from that formtool in the slider (`ftPrefix`, `ftSuffix`, etc).

The slider formtool adds 4 new metadata options. `ftMin`, `ftMax`, `ftStep`, and `ftOrientation`. Min and Max are the lowest and highest values allowed for the field. `ftStep` is the increment factor the slider will use. If you specify one, each slide of the slider will move the value by 1, if you specify 0.5, it will increment it by 0.5 (1, 1.5, 2, etc). `ftOrientation` can be either "horizontal" or "vertical" and it will orient the slider either horizontally or vertically.

Your users can either type a value into the text box or use the slider to select a value.

This uses the [jQuery UI Slider widget](http://jqueryui.com/demos/slider/) so you can use it with FarCry 6+ since core ships with jQuery UI built in.

If you find it useful, missing a feature, broken, etc please let me know. Consider it released under a "do whatever you want with it" license.