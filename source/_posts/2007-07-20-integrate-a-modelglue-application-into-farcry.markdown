---
layout: post
title: "Integrate a Model-Glue Application into FarCry"
date: 2007-07-20 13:04:00 -0400
comments: true
published: true
categories: [FarCry, Model-Glue]
---

I'm sure there are other ways to do this but 
this is how I was able to integrate an existing Model-Glue application 
into a FarCry site.  I am using ModelGlue 2.0, the latest ColdSpring BER 
as of this posting, and the latest beta of reactor.

My MG app in 
question is a events calendar.  Its a pretty simple application using 
MG, Reactor, and ColdSpring.

Because I don't want to use ColdFusion 
mappings (and its running on CF7 so no per application mappings) I 
copied modelglue, reactor, and coldspring into 
{farcry_root}/projects/{site_name}/www as www/modelglue, www/reactor, 
and www/coldspring.

If you are using mappings you can skip that step.

Next, I created a simple include file called _mgCal.cfm in 
{farcry_root}/projects/{site_name}/includedObj.

The code for this is 
as follows:

{% gist 8810571 %}

Now, in the FarCry 
webtop, under the site tab, navigate to the root node, and under 
utility, create a new navigation node called "Calendar" and under that, 
a new include called "Calendar".

Publish both.  The friendly URL 
should be /go/calendar, but it can be whatever you like.

Now we have 
to copy our MG application into the site tree.  Create a new folder 
called "mg" under the www folder.  This is where all my MG apps will 
live.  So I copy my "mgCal" folder from my test site into the "mg" 
folder I just created giving me a directory structure like 
so:

```
/www/mg/mgCal/
/www/mg/mgCal/config
/www/mg/mgCal/controller
/www/mg/mgCal/model
/www/mg/mgCal/views
/www/mg/mgCal/Application.cfm
/www/mg/mgCal/index.cfm
etc
```

Now 
we have a few modifications to make to the MG app to get it to run from 
this location.  Depending on how you first created the MG app, your 
settings may be different.

In your MG App's index.cfm file add the 
following line above the &lt;cfinclude&gt; that calls 
Model-Glue.

{% gist 8810594 %}

Now MG can find your ColdSpring 
configuration file.

In your ColdSpring configuration file edit the 
following properties:

In your modelGlueConfiguration bean:

The 
paths should be straight forward, but your defaultTemplate property must 
be set to the FriendlyURL of your include.

{% gist 8810609 %}

In 
your reactorConfiguration bean:

{% gist 8810621 %}

You 
will want the paths to match those you set up in the previous 
steps.

Now for the tedious part.  This was easy for me since I only 
have a few views, but a complex app with a large number of views will 
probably be a bit more work.

In each view that calls 
#viewState.getValue('myself')# you will have to, prior to any of those 
calls run the following statement:

{% gist 8810632 %}

This is to prevent a url like 
/go/calendar?event=some.mgEvent from happening.  The friendlyURL is 
hiding some other FarCry URL variables.  So there is already a ? in 
the URL.  This will replace the ? that MG creates with an ampersand so 
you can attach the MG url variables. easily. 

Thats all it took to get 
my simple calendar MG app running under FarCry.  A more complex app may 
need more to get running, but at least this will get you started.

If 
any one has any suggestions on a better way to handle this, I am all 
ears.  I tried to find another instance of someone doing this in both 
the [FarCry](http://groups.google.com/group/farcry-dev) and 
[Model-Glue](http://groups.google.com/group/Model-Glue) lists 
to no avail.