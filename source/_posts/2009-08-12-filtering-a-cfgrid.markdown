---
layout: post
title: "Filtering a CFGrid"
date: 2009-08-12 09:23:00 -0400
comments: true
published: true
categories: [ColdFusion, Web Development]
---

So you want to filter a CFGrid huh? ColdFusion makes this easy! First you need a CFC method that will return the query used to populate the grid. This method should take the cfgrid parameters and the value you want to filter on.

{% gist 8810170 %}

You can see here that I am just hard coding the query in, you would replace this with your cfquery call to your database or a call to your service layer, etc. Once you have your query results, you want to use the `queryConvertForGrid` function to format the result to a value that CFGrid can work with.

You then need a cfgrid! The trick here is how to get the grid to refresh as the user types a value in the filter box. ColdFusion Ajax UI tools have bind expressions that let us bind one control to another, and to react to events.

{% gist 8810199 %}

You can see my bind expression in the cf grid. It will call the getData method of my data.cfc and pass in the value from the "filter" input box whenever the key is released. ColdFusion provides other events you can react to as well, check the docs for details.

So now if you run index.cfm you will see a simple form with a text input and a grid. the grid will load when the page is run (`bindonload="true"`) and as you type in the text box, the results are filtered.

EDIT: removed the example link as I have moved this blog to [Railo](http://www.getrailo.org/)