---
layout: post
title: "Transfer Error when using ntext or text and a ManyToMany Relationship"
date: 2009-02-17 08:43:00 -0400
comments: true
published: true
categories: [ColdFusion, Transfer]
---

When you set Transfer to use a 
table that has an ntext or text column on SQL Server 2000 (and perhaps 
later versions) and also a many to many relationship you may receive the 
following error when you attempt to retreive the collection for the many 
to many:

{% gist 8810319 %}

For example I have the following tables set up

{% gist 8810330 %}

And the following transfer configuration:

{% gist 8810367 %}

So when you call getRelationArray() on a Table1 object.  You will receive 
the error.  To correct this I took the following steps:

Create a for table 1 with the ntext column casted to varchar:


	select id,title,cast(description as varchar(8000)) as description from table1

Save this as vwTable1.

Change your transfer config to point to the view instead of table one so	

{% gist 8810384 %}

becomes

{% gist 8810393 %}

Now, you wont be able to 
run it yet because the view is not updatable since you used the casted 
field.  To overcome this we are going to use an INSTEAD OF 
trigger.

You need to create 2 triggers.  One will be called 
whenever UPDATE is called on the vwTable1 and the other will be called 
when INSERT INTO is called on vwTable1

You can create the 
triggers as follows, obviously change it to suit your table's 
needs:

{% gist 8810433 %}

Once you have created these triggers you 
should be able to use Transfer as you normally would.  Using the casted 
column in the view will allow you to call the getRelationArray().  The 
SQL that Transfer creates will no longer be invalid.

You may run 
into a couple of other items though.  First, your ntext field is now 
limited to 8000 characters since you are casting it to varchar.  You may 
be able to increase this, but I haven't tried.  Your mileage may vary, 
but be sure before the value is passed to transfer that it is validated 
as less than 8000 characters (perhaps in your decorator).  Next, if you 
have any non-null, defaulted columns in your base table (a created date 
perhaps) you HAVE to provide a value when you call insert into vwTable1.  
Since Transfer is creating this SQL you have to ensure that Transfer 
includes that column.  This means that you cannot use the 
ignore-insert="true" option in the transfer configuration.  SQL Server 
will still respect your default value, as long as you provide that 
column in the sql statement pointed at the view.

You can find 
more information about [INSTEAD 
OF INSERT](http://msdn.microsoft.com/en-us/library/aa214478(SQL.80).aspx) and [INSTEAD 
OF UPDATE](http://msdn.microsoft.com/en-us/library/aa214430(SQL.80).aspx) triggers on the MSDN site.

I have only used this in 
a simple application with two base tables and one relationship table, so 
if your setup is more complex it may not work out for you.