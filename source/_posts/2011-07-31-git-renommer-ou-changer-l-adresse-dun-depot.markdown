---
comments: true
date: 2011-07-31 00:51:06
layout: post
slug: git-renommer-ou-changer-l-adresse-dun-depot
title: 'Git: Renommer ou changer l''adresse d''un dépôt'
wordpress_id: 989
categories:
- Development
tags:
- git
- github
---

Un p'tit coup de main qui vous fera gagner du temps si vous êtes nouveau à **Git**. ;)

Dans le répertoire local de votre projet, ouvrez le fichier _.git/config_, dans la catégorie _[remote "origin"]_, modifier le paramètre _url_ avec la nouvelle adresse ou le nouveau nom du dépôt. 

**OU**

Utilisez la commande suivante:
[bash]
git remote set-url origin <nouvelle adresse>
[/bash]



_Note:_ Si vous utilisez **GitHub**, il faut impérativement renommer le projet sur la plateforme: allez sur la page de votre dépôt, cliquez sur le bouton _Admin_, et changez le nom. 
