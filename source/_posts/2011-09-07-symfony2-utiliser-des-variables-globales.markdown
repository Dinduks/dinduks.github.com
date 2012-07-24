---
comments: true
date: 2011-09-07 03:43:46
layout: post
slug: symfony2-utiliser-des-variables-globales
title: 'Symfony2: Utiliser des variables globales'
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

Pour utiliser des variables dans un contrôleur *Symfony2*, il faut les déclarer dans *parameters.ini*, ou dans tout autre fichier *ini* à condition que vous l'importiez dans *config.yml*.
Au cas où vous voudrez les utiliser dans un template Twig, il faut les déclarer dans *config.yml*. ([Merci à Chris pour l'astuce](http://www.dinduks.com/symfony-2-utiliser-des-variables-globales#comment-577))

Vous pourrez alors les appeler avec `getParameter()` depuis un contrôleur ou avec la syntaxe `{{  }}` depuis un template *Twig*.


### Déclarer votre variable

Dans un fichier ini:

    [parameters]
        maVariable = 2

Ou dans _config.yml_:

    twig:
      globals:
        maVariableTwig: %maVariable%

### Importer votre fichier ini dans _config.yml_

Vous pouvez sauter cette étape si vous aviez déclaré la variable dans _parameters.ini_.

    imports:
        - { resource: monFichier.ini }

### Utiliser la variable globale

#### Dans un contrôleur:

    $maVariable = $this->container->getParameter('maVariable');

#### Dans un template Twig:

    <p>
        Ma variable: {{ maVariableTwig }}
    </p>

Enjoy. ;)
