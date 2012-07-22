---
comments: true
date: 2011-11-30 23:13:21
layout: post
slug: git-rename-or-change-a-repository-url
title: 'Git: Rename or change a repository URL'
wordpress_id: 1494
categories:
- Development
tags:
- git
- github
---

If you’re new to **Git**, this tip will allow you to save some of your precious time. 

Open _.git/config_ in your project’s local directory, and, in the category _[remote "origin"]_, modify the _url_ parameter, using the new location or the new repository’s name.

**OR**

Use this command: 
[bash]
git remote set-url origin <new url>
[/bash]



Note: If you’re using **GitHub**, you must also rename the project on the platform: Go to the repository's homepage, click the Admin button and change the name.





Translated from my french post [Git: Renommer ou changer l’adresse d’un dépôt](http://www.dinduks.com/git-renommer-ou-changer-l-adresse-dun-depot)
