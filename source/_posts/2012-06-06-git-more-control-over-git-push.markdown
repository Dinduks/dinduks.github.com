---
comments: true
date: 2012-06-06 16:35:29
layout: post
slug: git-more-control-over-git-push
title: 'Git: More control over git push'
wordpress_id: 2032
categories:
- Development
tags:
- git
---

I've recently had to do a `git push -f` which not only pushed the branch I'm on, but also all my other local branches, overriding the remote ones. 
Fortunately for my teammates and I, the other branches were not crucial. 

This behavior is due to Git's _[push.default](http://www.kernel.org/pub/software/scm/git/docs/v1.7.2.5/git-config.html)_ option set to _matching_, which means _Push all matching branches_. That's nonsense to me considering the problems it may cause. 

This can be changed of course, by setting the _push.default_ to another value: 





  * **nothing** do not push anything.


  * **matching** push all matching branches. All branches having the same name in both ends are considered to be matching. This is the default.


  * **tracking** push the current branch to its upstream branch.


  * **current** push the current branch to a branch of the same name.



The most suitable option in most of situations, in my opinion, is the _tracking_ option.

Happy versionning and be careful!
