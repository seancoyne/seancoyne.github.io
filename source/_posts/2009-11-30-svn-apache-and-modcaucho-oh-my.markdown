---
layout: post
title: "SVN, Apache, and mod_caucho, oh my"
date: 2009-11-30 11:01:00 -0400
comments: true
published: true
categories: [Apache, Railo, Subversion]
---

I recently set up a new [Viviotech](http://www.viviotech.net/?rid=n42designs) VPS and ran into an issue that was easy to fix once I realized what was happening, but difficult to debug.

I set up Railo running on the Resin server using Apache as a front end with mod_caucho. In my `httpd.conf` file I had the following lines:

{% gist 8810530 %}

This causes Resin to handle all requests from apache. The resin configuration files tell resin which URLs to handle. I also had an SVN server set up so I had a configuration file in `/etc/httpd/conf.d/` to set up subversion. All my SVN repositories are under the location `/svn`. Reading SVN repositories worked fine, but I kept getting "path not found" errors when committing new files. After debugging this for quite a while using Fiddler, and other means, I finally realized that Resin was actually handling the PUT http request and, finding no file, returned a 404.

So to fix this, and simply have Apache handle any request to `/svn/` I modifed my `httpd.conf` file as follows:

{% gist 8810539 %}

then restarted Apache.  Now apache handles any requests to `/svn/*` and Resin handles all other requests. Hopefully this helps future Googlers in need.