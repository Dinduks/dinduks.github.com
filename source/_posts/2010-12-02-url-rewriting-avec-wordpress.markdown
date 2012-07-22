---
comments: true
date: 2010-12-02 14:08:24
layout: post
slug: url-rewriting-avec-wordpress
title: L'URL Rewriting avec Wordpress
wordpress_id: 359
categories:
- Tutorials
tags:
- url rewriting
- wordpress
---

#### L'**URL Rewriting**, c'est quoi?



L'**URL Rewriting** est une technique qui permet non seulement de réécrire les urls pour les simplifier, mais aussi d'améliorer le **référencement** de votre site.
Votre url va alors ressembler à ça _http://www.dinduks.com/url-rewriting-avec-wordpress_ au lieu de _http://www.dinduks.com/?p=359_.



![L'URL Rewriting avec Wordpress](/wp-content/images/wordpress-url-rewriting.png)






#### Comment l'activer?



Il suffit de vous rendre sur la page **[Permaliens](http://www.dinduks.com/wp-admin/options-general.php)** dans les Réglages de votre blog **Wordpress**, de sélectionner "Structure personnalisée", et finalement mettre le tag suivant dans le champ qui nous intéresse: **_/%postname%_**

Ce tag indique au blog qu'il faut afficher les liens sous cette forme: _domaine.com/titre-du-post_.
La syntaxe est personnalisable à souhait, une multitude d'autres tags est disponible sur [le Codex de **Wordpress**](http://codex.wordpress.org/Using_Permalinks).



#### Performances



L'utilisation de l'**URL Rewriting** peut avoir un impact néfaste sur les performances, consultez [cet article](http://bit.ly/g2LDxu) pour plus d'informations.
