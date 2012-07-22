---
comments: true
date: 2011-06-22 21:20:45
layout: post
slug: svn-arret-de-la-propagation
title: 'SVN: Arrêt de la propagation : ''/chemin'' demeure en conflit'
wordpress_id: 919
categories:
- Development
- Pieces of code
tags:
- subversion
- svn
---

Si vous avez cette erreur, essayez: 



#### Dans le cas d'un dossier: 


[bash]
svn resolved -R chemin/
[/bash]



#### Dans le cas d'un fichier


[bash]
svn resolved chemin/fichier
[/bash] 
