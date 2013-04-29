---
comments: true
date: 2011-12-05 22:50:06
layout: post
slug: symfony-2-using-global-variables
title: 'Symfony 2: Using global variables'
categories:
- Development
- Pieces of code
- Symfony 2
tags:
- php
- symfony
- symfony2t
- twig
---

In order to use variables in a **Symfony2** controller, you’ll have to set them up in *parameters.ini*, or in any other ini file on condition that you’ll import it into *config.yml*.  
In case you want to use them in a Twig template, you must set them up in *config.yml*.

Once done, you’ll be able to whether call them using `getParameter()` from a controller or with the syntax `{{ }}` from a Twig template.

#### Set up your variable

In an ini file:

    [parameters]
        myVariable = 2

In *config.yml*:

    twig:
      globals:
        myTwigVariable: %myVariable%

#### Import your ini file into config.yml

You can skip this step if you already set up the variables in *parameters.ini*.

    imports:
        - { resource: myFile.ini }

#### Use the global variable

In a controller:

    $myVariable = $this->container->getParameter('myVariable');

In a Twig template

    <p>
        My variable: {{ myTwigVariable }}
    </p>

Enjoy. ;)

*Translated from my french post [Symfony2: Utiliser des variables globales](http://www.dinduks.com/symfony2-utiliser-des-variables-globales)*
