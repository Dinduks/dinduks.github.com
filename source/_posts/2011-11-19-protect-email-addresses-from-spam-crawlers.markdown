---
comments: true
date: 2011-11-19 19:23:35
layout: post
slug: protect-email-addresses-from-spam-crawlers
title: Protect email addresses from spam crawlers
wordpress_id: 1397
categories:
- Development
- Tutorials
tags:
- email address
- php
- spam crawlers
- twig
---

Hi, 

When displaying a raw email address on a Web page, this address is vulnerable and can be used by _spam crawlers_, _email harvester_, or whatever you want to call them to send you spam and such crap. 
That's why people write their email address this way "samy at dindane dot com", or "samy[@]dindane[.]com". 
This writing is simple and efficient, but not _pretty_. 

There are many ways to show an email address in its original format and still make it bots-proof. One of these ways is using JavaScript to obfuscate and then show the address. 
But I think that using JS is overdoing things, since it can be done using basic HTML, simply by printing the email address as ASCII and not raw characters.



#### These are the steps to follow using PHP:






  * 
Split the email address into an array of characters

    
    
    $aEmail = str_split($email);
    





  * 
Convert each character into an ASCII one:

    
    
    $strEmail = '';
    foreach ($aEmail as $char) {
        $strEmail .= ord($char);
    }
    





  * 
Display it (O RLY?):

    
    
    echo "<a href='$strEmail'>$strEmail</a>";
    






The result is a beautiful and clickable email address. :)

**Note:** If you are using **Twig** as a template engine, you have to use the _raw_ filter in order to tell Twig to interpret the string and not to display raw ASCII characters : **{{ strEmail|raw }}**

I hope this tutorial has been helpful. 
Bye!
