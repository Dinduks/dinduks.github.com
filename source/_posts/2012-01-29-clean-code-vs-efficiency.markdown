---
comments: true
date: 2012-01-29 15:42:22
layout: post
slug: clean-code-vs-efficiency
title: Clean code vs Efficiency
categories:
- Development
tags:
- efficiency
- good practices
- php
- symfony2
---

I have recently submitted [my first pull request](https://github.com/symfony/symfony/pull/3209) ever, to the Symfony2 project.

[The code I contributed with](https://github.com/Dinduks/symfony/commit/5306457f4b1073c6544dd4235a74c4d5f612ed9d) is a 3 lines long method that simply checks whether a form field is hidden or not.
I have no doubt about the usefulness of this method, especially after seeing few people using a similar one (it seems that it was removed).

The pull request was [refused](https://github.com/symfony/symfony/pull/3209#issuecomment-3707718) because the class in question isn't supposed to be *aware of information we need*.
I agree with this and approve the good practices and clean code, but in this case we penalize the end user for the sake of doing things the *right* way.

The purpose of my post is to answer the following question: should efficiency and simplicity be sacrificed for the sake of good practices and clean code?

In my opinion, the answer is no. Especially when we're dealing with a big project that thousands of people use, and that claims easiness and simplicity.

I'm looking forward to know your opinion about the subject. Feel free to leave a comment.

{% img center /uploads/2012/01/programming-motherfucker.jpg '' 'Programming Motherfucker' %}
