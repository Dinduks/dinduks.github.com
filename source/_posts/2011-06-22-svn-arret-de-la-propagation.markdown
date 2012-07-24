---
comments: true
date: 2011-06-22 21:20:45
layout: post
slug: svn-arret-de-la-propagation
title: 'SVN: Arrêt de la propagation : ''/chemin'' demeure en conflit'
categories:
- Development
- Pieces of code
tags:
- subversion
- svn
---

Si vous avez cette erreur, essayez:

#### Dans le cas d'un dossier:

    svn resolved -R chemin/

#### Dans le cas d'un fichier

    svn resolved chemin/fichier
