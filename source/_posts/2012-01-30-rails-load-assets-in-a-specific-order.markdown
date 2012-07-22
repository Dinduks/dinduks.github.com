---
comments: true
date: 2012-01-30 23:57:22
layout: post
slug: rails-load-assets-in-a-specific-order
title: 'Rails: Load assets in a specific order'
wordpress_id: 1929
categories:
- Development
- Pieces of code
- Rails
tags:
- assets
- rails
---

Let's pretend you have many CSS/SASS stylesheets and JS/Coffee scripts in your project, and you want to load some before the rest. 
This can be done in `stylesheets/application.css` and `javascripts/application.js` by using the keyword `require`. 



### Examples:




#### Stylesheets: 


If you want to load Bootstrap's stylesheet first: 




#### Javascripts: 


This is how to load jQuery and Boostrap's scripts before the others: 


You can omit the files extensions. 

I believe they call this the awesomeness of Rails. 
