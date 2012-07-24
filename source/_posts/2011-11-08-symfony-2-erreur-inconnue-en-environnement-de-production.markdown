---
comments: true
date: 2011-11-08 14:44:23
layout: post
slug: symfony-2-erreur-inconnue-en-environnement-de-production
title: 'Symfony2: Erreur inconnue en environnement de production'
categories:
- Symfony 2
tags:
- php
- symfony2
---

Ce billet est une note pour ceux qui tomberaient un jour dans ce genre de situations.

J'ai créé un contrôleur qui me renvoie la réponse attendue lorsque je suis en environnement de dev (_site/app_dev.php/foo/bar_), mais j'ai une page blanche en prod (_site/foo/bar_).  
Rien dans le fichier de logs (_/logs/prod.log_), même pas une nouvelle ligne quand j'accède à la page.  

Ne sachant plus quoi faire, je décide de nettoyer le cache de prod, et c'est justement ce dernier qui m'indique la source de mon problème. J'avais en effet changé le nom d'un Entity Manager, et j'ai oublié de mettre à jour quelques lignes dans _app/config/config_prod.yml_.  
Celle-ci n'est évidemment pas l'unique raison possible, mais nous montre qu'une erreur peut survenir de n'importe où, que Symfony 2 ne nous montre pas toujours les erreurs, et qu'un nettoyage du cache peut le faire à sa place.

Morale du jour: un php `app/console cache:clear --env="prod"` après des heures de travail ne fait de mal à personne! :)
