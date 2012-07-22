---
comments: true
date: 2011-11-17 20:19:51
layout: post
slug: symfony-2-render-helper-for-calling-an-action-from-a-view
title: 'Symfony2: "render" helper for calling an action from a view'
wordpress_id: 1368
categories:
- Development
- Pieces of code
- Symfony 2
tags:
- php
- symfony
- symfony2
- twig
---

I discovered some days ago a _secret_ Symfony 2's helper. I call it secret because I can't find it anywhere on the documentation.
_Edit: Here it is on the Symfony2 book: [Embedding Controllers](http://symfony.com/doc/2.0/book/templating.html#embedding-controllers)_

_{% **render** %}_ is used to show an action's response in a **Twig** template. It's very useful when wanting to show a dynamic content in all the app's pages.

**Example:** Displaying online users' counter.





  * 
First of all we have to create a _onlineUsersAction()_ function that fetches, processes the result and returns the counter of the online users.




  * 
Then we gotta create a Twig template that displays the response returned by the action. The syntax is the following: 
    
    {% render "LiveGeekBundle:Default:onlineUsers" %}


Knowing that _onlineUsersAction()_ is an action of _DefaultController_ which is a controller from the _Live\GeekBundle_ bundle.




  * 
Finally we must include that template in our application's default layout, and thus display the online users' counter in all the app's pages.





**Passing arguments:**
You can pass arguments to the action this way:




  * 
In the Twig template:

    
    {% render "LiveGeekBundle:Default:onlineUsers" with { 'arg1' : 'value1', 'arg2' : 'value2' } %}






  * 
In the controller: 
[php]
helloAction($arg1, $arg2) 
[/php]
Or
[php]
helloAction($arg2, $arg1)
[/php]
The arguments' order doesn't matter.


Enjoy. ;)
