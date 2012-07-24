---
comments: true
date: 2012-01-06 23:22:23
layout: post
slug: a-question-about-applications-design
title: A question about applications' design
categories:
- Development
tags:
- architecture
- rails
---

The idea of creating a blog post to gather people's opinions is pretty weird, but *nothing ventured, nothing gained*.



Hello,

I'm building an application that will have many types of multilingual dynamic content: news, about, announces, meta tags, meta description, and maybe more.
The app is a **Rails** one, so I'll be talking about tables and not entities.

I've been creating a database table for each of the content types above, and I noticed halfway that they have (almost) the same columns: *title*, *body*, *lang_id*.
I decided then to use one single table, called *text*, which will have a *text_type_id* column, additionally to all the previous columns. *type_text* will only contain the type of the content (news, about, announce, etc...).

The thing is that I'm not very convinced about what I've done, I find it a bit dirty because many kind of data will be stored in the same place. On the other hand, if I create a table for each type, it seems to me that there will be some kind of redundancy, which is also messy in my eyes.

What do you think about this? Please leave a comment explaining what you would have done if you were in my shoes, and why.

Thanks!
