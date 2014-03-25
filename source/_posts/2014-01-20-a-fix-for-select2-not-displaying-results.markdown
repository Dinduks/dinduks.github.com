---
layout: post
title: "A fix for Select2 not displaying results on IE"
date: 2014-01-20 17:47
comments: true
categories: 
---

When using Select2, filling a select box, and not seeing any result, chances are
that you're querying a different server, which requires CORS, which in turn
isn't supported by Internet Explorer (9.0 and below).  

Using the [jQuery-ajaxTransport-XDomainRequest](
https://github.com/MoonScript/jQuery-ajaxTransport-XDomainRequest) plugin fixes
the problem.  
Explanations are in the README.

(this problem is of course not specific to Select2, but given the layers of
code/libs between the developer and the creation oFJthe XHR object inside
jQuery's `ajax()` function, one might forget this detail like I did)
