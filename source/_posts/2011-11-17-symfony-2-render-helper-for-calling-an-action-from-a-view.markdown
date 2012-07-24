---
comments: true
date: 2011-11-17 20:19:51
layout: post
slug: symfony-2-render-helper-for-calling-an-action-from-a-view
title: 'Symfony2: "render" helper for calling an action from a view'
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

I discovered some days ago a *secret* Symfony 2's helper. I call it secret because I can't find it anywhere on the documentation.  
*Edit: Here it is on the Symfony2 book: [Embedding Controllers](http://symfony.com/doc/2.0/book/templating.html#embedding-controllers)*

`{% render %}` is used to show an action's response in a *Twig* template. It's very useful when wanting to show a dynamic content in all the app's pages.

### Example: Displaying online users' counter

#### Create a `onlineUsersAction()` function
That function fetches, processes the result and returns the counter of the online users.

#### Create a Twig template that displays the response returned by the action
The syntax is the following:

      {% render "LiveGeekBundle:Default:onlineUsers" %}

Knowing that `onlineUsersAction()` is an action of `DefaultController` which is a controller from the *Live\GeekBundle* bundle.

#### Include that template in our application's default layout
Thus display the online users' counter in all the app's pages.

### Passing arguments:
You can pass arguments to the action this way:

#### In the Twig template:

    {% render "LiveGeekBundle:Default:onlineUsers" with { 'arg1' : 'value1', 'arg2' : 'value2' } %}

#### In the controller:

    helloAction($arg1, $arg2)

Or

    helloAction($arg2, $arg1)

The arguments' order doesn't matter.

Enjoy. ;)
