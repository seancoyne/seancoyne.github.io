---
layout: post
title: "Issue w/ Eclipse Resource Bundle Editor Plugin and Leopard"
date: 2008-01-17 16:18:00 -0400
comments: true
published: true
categories: [Eclipse, Web Development]
---

There seems to be an issue with the [Resource Bundle Editor Plugin for Eclipse](http://sourceforge.net/projects/eclipse-rbe/).

I installed version 0.7.7 into a fresh install of the Eclipse 3.3 SDK and was unable to open a resource file.  I would get the following error:

{% blockquote %}
Can't start the AWT because Java was started on the first thread.  Make sure StartOnFirstThread is not specified in your application's Info.plist or on the command line
{% endblockquote %}

To fix it I edited the `eclipse.ini` file (`/Applications/eclipse/Eclipse.app/Contents/MacOS/eclipse.ini` by default) to add the following line:

`-Djava.awt.headless=true`

Once I did that it was fine and I was able to edit the resource bundles.

Hope this helps someone searching for the issue!