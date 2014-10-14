---
layout: post
title: "ValidatorCFC"
date: 2007-07-20 23:30:00 -0400
comments: true
published: true
categories: [ValidatorCFC]
---

This component validates the data in an object according to custom rules you set up.  It is especially created to determine data validity for a data store (DBMS, etc) rather than for business rules, but you can set up your own complex rules.  Some may be out of its scope, however.

I just uploaded version 0.1.000.  It is very much a work in progress and I welcome feedback.

Take a look and let me know what you think.  You can find it at [http://validatorCFC.riaforge.org](http://validatorcfc.riaforge.org) or at the download link below.

Here is a rundown of an example usage:

<!-- more -->

First, Create an instance of this object.  It should not be in any shared scope as its not thread safe.

{% gist 8810676 %}
		
Next, take whatever data you want to validate and put it in an object that follows some rules.

You  must use cfproperty tags to define what rules, whether it is required or not, and messages to use.

You must create getters for each property like getFirstName() where FirstName is an example property name.

You can specify any number of rules for each property in a comma separated list.  Each rule should be a CFC in the rules subfolder and should extend the _rule.cfc base object.

{% gist 8810696 %}

where testObj is a component defined as follows: (yes I know that my setGPA function allows for setting an obviously numeric property with a string value, this is for example only)
		
{% gist 8810752 %}

Now, pass this object to the validator component validate function to perform the validation

{% gist 8810764 %}
	
Use the getValid() and getMessages() functions to work with the data.

{% gist 8810775 %}

If you want to reuse this instance run init() function. If you are not going to reuse then this is optional.
	
{% gist 8810788 %}