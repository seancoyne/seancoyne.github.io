---
layout: post
title: "Github Gist renderer for BlogCFC"
date: 2012-02-12 14:47:00 -0400
comments: true
published: true
categories: [ColdFusion]
---

I created a quick renderer for Github Gists for use within <a href="http://www.blogcfc.com/" target="_blank">BlogCFC</a> entries. You can see it in action right here. If interested just grab the code from the gist below and save it to /org/camden/blog/render/gist.cfc. You can then use

{% gist 8810495 %}

to include the gist in your entry. If you want to constrain the height you can use CSS like:

{% gist 8810484 %}

Here is an example of what the output looks like, using the Gist I created to hold the code for the renderer.  Feel free to grab it for your own BlogCFC install.

{% gist 1810183 %}