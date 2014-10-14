---
layout: post
title: "FarCry YouTube Plugin"
date: 2011-08-08 17:22:00 -0400
comments: true
published: true
categories: [ColdFusion, FarCry]
---

One of our clients asked for better integration of their YouTube hosted videos on their FarCry website.  They had been linking to the youtube.com URLs directly, leading traffic away from their website.  Obviously, they would have preferred to keep those visitors on their site and engaged.

As some other clients have also expressed a desire to display YouTube videos on their sites, I decided to build the functionality as a FarCry plugin.  This would allow me to move this feature set to any FarCry site.

At its foundation, the plugin works via two custom types and a scheduled task.  The scheduled task runs and uses the YouTube API to grab the playlists and videos on the specified account (configurable via a FarCry config).  If it finds those objects already in FarCry, it updates them with the latest data from YouTube, if its new, it adds it to the FarCry database.  Any items found in FarCry that aren't returned by the API are deleted.  The plugin gives you the ability to reorder the videos on a playlist via the FarCry webtop.  All data is managed on the YouTube side.  I may consider adding the ability to completely manage the videos and playlists on the webtop, but that will greatly increase the complexity of the plugin, and I don't see a great benefit to doing so.  To me, it makes more sense to go straight to the source to upload new videos, manage your videos, etc rather than try to stuff all that functionality into a FarCry form.  No need to reinvent the wheel, in my opinion.

The plugin also includes two rules.  One lists videos based on selected playlists or videos, the other displays an embedded video.

To interact with the YouTube API, I made use of [Raymond Camden](http://www.coldfusionjedi.com/)'s awesome [YouTube CFC](http://youtubecfc.riaforge.org/).

I am happy to say that I have also posted this code on Github for the entire community to use.  Give it a try!  If you have any ideas for improvement please open a ticket, or better yet, fork the project and send me a pull request.

You can find the project on [RIAForge](http://farcryyoutube.riaforge.org/) and [Github](https://github.com/seancoyne/FarCry-YouTube-Plugin).