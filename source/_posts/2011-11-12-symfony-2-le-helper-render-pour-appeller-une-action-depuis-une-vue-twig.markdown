---
comments: true
date: 2011-11-12 23:40:19
layout: post
slug: symfony-2-le-helper-render-pour-appeller-une-action-depuis-une-vue-twig
title: 'Symfony2: Le helper render pour appeller une action depuis une vue Twig'
wordpress_id: 1325
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

Aujourd'hui j'ai découvert un helper _secret_ de **Symfony 2**. Secret parce que je ne le retrouve nulle part sur la doc. 
_Edit: On en parle sur la doc Symfony2: [Embedding Controllers](http://symfony.com/doc/2.0/book/templating.html#embedding-controllers)_

_{% **render** %}_ sert à afficher la réponse d'une action dans un template **Twig**. C'est surtout utile quand on veut afficher du contenu dynamique dans toutes les pages de notre application. 

Exemple d'utilisation: Je veux afficher le nombre des utilisateurs connectés.




  * Je crée une action _onlineUsersAction()_ qui fait le traitement


  * Je crée un template Twig qui affiche la réponse retournée par l'action. La syntaxe est la suivante: 
    
    {% render "LiveGeekBundle:Default:onlineUsers" %}


Sachant que _onlineUsersAction()_ est une action de _DefaultController_ qui est lui même un contrôleur du bundle _Live\GeekBundle_.


  * J'inclue ce template dans le layout de l'appli et affiche ainsi le nombre des utilisateurs connectés dans toutes mes pages.



**Passer des arguments:**
Vous pouvez passer des arguments à l'action de cette manière:




  * 
Dans le template Twig:

    
    {% render "LiveGeekBundle:Default:onlineUsers" with { 'arg1' : 'value1', 'arg2' : 'value2' } %}






  * 
Dans le contrôleur: 
[php]
helloAction($arg1, $arg2) 
[/php]
Ou
[php]
helloAction($arg2, $arg1)
[/php]
L'ordre des arguments ne compte pas.


Enjoy. ;)
