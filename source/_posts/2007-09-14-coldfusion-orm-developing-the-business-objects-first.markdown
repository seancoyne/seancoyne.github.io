---
layout: post
title: "ColdFusion ORM - Developing the Business Objects First"
date: 2007-09-14 07:12:00 -0400
comments: true
published: true
categories: [ColdFusion]
---

Since I have transitioned from a world of 
spaghetti code through the land of the uber-cfc, and finally onto some 
OO concepts, I have tried to figure out what the best way to create the 
business objects and persist them to the database.  For nearly ever 
application I have developed, I have created the database first, since, 
in my mind, understanding the data is the first step to understanding 
the way the application will function.

However, in the OO world, 
the primary step is to design the business objects.  In my latest 
project I decided to take one step deeper into the OO world and develop 
all my business objects forgetting all about how the database would be 
laid out.  I had no problems with this, authoring complex objects 
containing arrays or instances of other objects without 
issue.

Then I needed to figure out how to persist them.  In the 
past, each of my business objects directly mapped to a table in my 
database.  This made it easy to build a code generator, read in the DB 
metadata and, in the words of John Madden, "Boom", I had my beans, DAOs, 
and Gateways.

Now, I see what Sean Corfield refers to as the "5:1 
Syndrome".  I have a dumb bean object, a DAO, a Gateway, a Service and, 
if using Model-Glue, a Controller for nearly every object, and in turn 
every table in the database. This always seemed like code bloat to me, 
so I was very happy to see other, like Sean, refer to it as such.  There 
must be a better way!

Trying to avoid this I decided, OK I'll 
use Reactor.  Active Record, generated code, sounds good.  Then I 
realized that I have to create the database first.  Back to square 
one.

Should business objects reflect the organization of the 
database?  They can, but if it doesn't fit the way the business object 
is used in the application, then no, it shouldn't.  Also, from the 
other way, the best way to organized the business objects is probably 
not the best way to organize the database.  The database should be in 
3NF, avoid duplication whereever possible, etc, etc.

Not wanting 
to trash all the BOs I created already, I decided I would write all the 
persistance stuff myself.  So now that I have some beans, I created a 
service for each and wired them up in ColdSpring.  I put all the methods 
that would normally go in my DAO (save, new, and CRUD) in my service as 
well as some getAll() calls.

As a side note, I don't return 
query objects since, even though they are faster than creating an array 
of objects, I cant call a complex getter, such as a calculated value 
easily, and this allows me to use the same calls to get the data for one 
instance of an object as I do for a collection.

Now I have a BO 
and a service that is completely separate from the DB.  Persisting 
complex objects is a bit more complicated than using the 1:1 BO to DB 
mapping, but it works.  The only issue is, I don't want to have to 
maintain all this manually.  I wish we had a mapping tool to handle 
persistance from BO to DB without requiring that the DB reflect the BO 
or vice versa.

Java has <a href="http://www.hibernate.org/" target="_blank">Hibernate</a> to handle this issue.  With CF8 [we 
can now use Hibernate](http://www.firemoss.com/blog/index.cfm?mode=entry&amp;entry=E3BB2C56-3048-55C9-439841683FDAA4D3) with a Java model, but what if we want to 
model using CFCs?  [cfHibernate](http://www.mattwoodward.com/blog/index.cfm?event=showEntry&amp;entryID=0192EC2E-A75D-7689-3A0C5ABFB71258AC) 
attempted to do this and seems to have run into some issues.  Can we use 
Hibernate to map CF objects to the DB?  I am going to attempt to find an 
answer for this in the next few weeks for my current project.  Hopefully 
I can find a solution.