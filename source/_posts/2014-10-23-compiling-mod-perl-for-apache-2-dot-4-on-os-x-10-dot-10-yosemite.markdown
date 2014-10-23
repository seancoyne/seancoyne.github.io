---
layout: post
title: "Compiling mod_perl for Apache 2.4 on OS X 10.10 Yosemite"
date: 2014-10-23 11:10:37 -0400
comments: true
categories: [Apache]
---

TL;DR: For your convenience, if you would like a pre-compiled binary you can download one [here](https://www.dropbox.com/s/euqfc0ivu1vx2vp/mod_perl.so.zip?dl=1).  This is the module I compiled.  I haven't tested it on any other systems than the one I compiled it with. YMMV.

* * *

OS X 10.10 Yosemite upgrades the default Apache install from 2.2 in Mavericks to 2.4.  In general, this is a good thing, but if you were using mod\_perl, perhaps for [mod_cfml](http://www.modcfml.org) with Railo for example, then mod\_perl will no longer work.

Recently, there have been several [commits](https://github.com/apache/mod_perl/commit/6e33d7c9e89afbdb47da0cb0fa9498d8a843df8e) so mod\_perl will now support Apache 2.4.  Since there are no binary releases yet, we will have to compile it ourselves.

I have managed to do this with help from [this StackOverflow post](http://stackoverflow.com/a/26497435/151136).

First you need the latest source from the Apache SVN repositories.  They mirror it on git, but its missing some dependencies, so I found it easier to use SVN.

`svn checkout https://svn.apache.org/repos/asf/perl/modperl/trunk/ mod_perl-2.0`

Then switch into the new directory:

`cd mod_perl-2.0`

Next, we need to be sure we have [XCode 6.1](https://itunes.apple.com/us/app/xcode/id497799835?mt=12) installed and the command line tools installed as well:

`xcode-select --install`

Once, we have that, we need to tell the compiler where to find a few dependencies.  You can find the reasoning behind this in the StackOverflow post mentioned above, but in general you run:

```bash
/usr/bin/apr-1-config --includedir /usr/include/apr-1
sudo ln -s /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.10.sdk/usr/include/apache2 /usr/include/apache2
sudo ln -s /Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.10.sdk/usr/include/apr-1 /usr/include/apr-1
```

This will create a couple simlinks and tell the compiler where some Apache headers are located.

Almost done.  Next, we compile it.  We need to set a compiler option to tell it to build using the gnu89 standard, instead of clang's default C99. (Thanks to [this blog post](http://blogs.perl.org/users/jason_a_crome/2012/04/compiling-mod-perl-2-on-os-x-lion.html) for that little nugget!)

`perl Makefile.PL MP_CCOPTS=-std=gnu89 ; make ; sudo make install`

This will install mod\_perl.so to `/usr/libexec/mod_perl.so`

Lastly, we need to tell Apache to load the newly compiled module and restart apache.  Add this line to your `/etc/apache2/httpd.conf` file:

`LoadModule perl_module libexec/apache2/mod_perl.so`

Then restart apache:

```bash
sudo apachectl configtest
sudo apachectl restart
```

If all is well, you should have a working mod\_perl module inside Apache 2.4.
