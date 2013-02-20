---
layout: post
title: "WebSockets: INVALID_STATE_ERR: DOM Exception 11"
date: 2013-02-18 09:34
comments: true
categories: 
---

This error can be caused by many reasons, among them what happened to me: I tried
sending a message via the WebSocket before the connection was completely opened.

What you should _not_ do:

    ws = new WebSocket("ws://localhost/ws");
    ws.send('foo');

What you should do instead:

    ws = new WebSocket("ws://localhost/ws");
    ws.onopen = function () {
      ws.send('foo');
    }
