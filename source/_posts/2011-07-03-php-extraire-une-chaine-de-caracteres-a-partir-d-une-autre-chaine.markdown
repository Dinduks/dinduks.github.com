---
comments: true
date: 2011-07-03 18:19:35
layout: post
slug: php-extraire-une-chaine-de-caracteres-a-partir-d-une-autre-chaine
title: 'PHP: Extraire une chaîne de caractères à partir d''une autre chaîne'
wordpress_id: 928
categories:
- Development
- Pieces of code
tags:
- php
- regex
---

Salut! 
[php]
echo $_SERVER["SERVER_SOFTWARE"];
// Retourne Apache/2.2.19 (Win32) PHP/5.3.6
[/php]

Disons qu'on veut récupérer la version d'**Apache** et de **PHP** à partir de cette chaîne. Le principe est d'utiliser la fonction [**preg_replace**()](http://php.net/manual/fr/function.preg-replace.php) pour éliminer tout ce dont a pas besoin. 


Dans notre exemple, pour la version de PHP, c'est plutôt puisqu'il suffit d'éliminer tout ce qui la précède:
[php]
$phpVersion = preg_replace("/.*?PHP\//", "", $_SERVER["SERVER_SOFTWARE"]);
[/php]

Ca change légèrement pour la version d'Apache, puisqu'on doit se débarrasser du texte entourant la version. Dans ce cas, au lieu de passer un seul motif **regex** dans une chaîne, on va passer les motifs des chaînes des deux côtés de la version dans un tableau:
[php]
$apacheVersion = preg_replace(array("/Apache\//", "/ \(.*/"), "", $_SERVER["SERVER_SOFTWARE"]);
[/php]




J'ai utilisé ces bouts de code pour faire une page d'accueil pour mon _localhost/_, dans le style de la page d'accueil de **WAMP**. Voici le lien pour les intéressés: [Dinduks' Web Workspace](http://pastebin.com/DDsQvFxp). ;)
