---
comments: true
date: 2011-09-07 03:43:46
layout: post
slug: symfony2-utiliser-des-variables-globales
title: 'Symfony2: Utiliser des variables globales'
wordpress_id: 1155
categories:
- Development
- Pieces of code
- Symfony 2
tags:
- php
- symfony
- symfony2
- twig
---

Pour utiliser des variables dans un contrôleur **Symfony2**, il faut les déclarer dans _parameters.ini_, ou dans tout autre fichier **ini** à condition que vous l'importiez dans _config.yml_. 
Au cas où vous voudrez les utiliser dans un template Twig, il faut les déclarer dans _config.yml_. ([Merci à Chris pour l'astuce](http://www.dinduks.com/symfony-2-utiliser-des-variables-globales#comment-577))

Vous pourrez alors les appeler avec _getParameter()_ depuis un contrôleur ou avec la syntaxe _{{  }}_ depuis un template **Twig**. 



  * Déclarer votre variable

Dans un fichier ini:
[ini]
[parameters]
    maVariable = 2
[/ini]

Dans _config.yml_:
[yml]
twig:
  globals:
    maVariableTwig: %maVariable%
[/yml]



  * Importer votre fichier ini dans _config.yml_

Vous pouvez sauter cette étape si vous aviez déclaré la variable dans _parameters.ini_.
[yml]
imports:
    - { resource: monFichier.ini }
[/yml]



  * Utiliser la variable globale

Dans un contrôleur: 
[php]
$maVariable = $this->container->getParameter('maVariable');
[/php]

Dans un template Twig:
[html]
<p>
    Ma variable: {{ maVariableTwig }}
</p>
[/html]

Enjoy. ;)
